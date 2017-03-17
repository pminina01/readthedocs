## Content
* [[Installing NLog|tutorial#installing-nlog]]
* [[Creating Log messages|tutorial#creating-log-messages]]
 * [[Creating loggers|tutorial#creating-loggers]]
 * [[Log levels|tutorial#log-levels]]
 * [[Writing log messages|tutorial#writing-log-messages]]
* [[Configuration|tutorial#configuration]]
 * [[Multiple targets|tutorial#multiple-targets]]
 * [[Logger-specific routing|tutorial#logger-specific-routing]]
 * [[Wrappers|tutorial#wrappers]]
 * [[Layouts|tutorial#layouts]]
* [[Advanced|tutorial#advanced]]

## Installing NLog
[NLog](https://www.nuget.org/packages/NLog/) can be downloaded from NuGet.

Just install [NLog.Config package](https://www.nuget.org/packages/NLog.Config/) and this will install also [NLog](https://www.nuget.org/packages/NLog) and [NLog.Schema](https://www.nuget.org/packages/NLog.Schema) packages - this will result in a starter config and intellisense.

Use the GUI or the following command in the Package Manager Console:
```
Install-Package NLog.Config
```

That's it, you can now compile and run your application and it will be able to use NLog.

## Creating Log messages
In order to create log messages from the application you need to use the logging API. There are two classes that you will be using the most: `Logger` and `LogManager`, both in the NLog namespace. `Logger` represents the named source of logs and has methods to emit log messages, and `LogManager` creates and manages instances of loggers.

It is important to understand that `Logger` does not represent any particular log output (and thus is never tied to a particular log file, etc.) but is only a source, which typically corresponds to a class in your code. Mapping from log sources to outputs is defined separately through [Configuration File](Configuration-file) or [Configuration API](Configuration-API). Maintaining this separation lets you keep logging statements in your code and easily change how and where the logs are written, just by updating the configuration in one place.

### Creating loggers
It is advised to create one (`private static`) `Logger` per class.  As mentioned before, you must use `LogManager` to create `Logger` instances.

This will create a `Logger` instance with the same name of the `class`.

```csharp
namespace MyNamespace
{
  public class MyClass
  {
    private static Logger logger = LogManager.GetCurrentClassLogger();
  }
}
```

It's also possible to control the `Logger`'s name:


```csharp
using NLog;

Logger logger = LogManager.GetLogger("MyClassName");
```

Because loggers are thread-safe, you can simply create the logger once and store it in a `static` variable.



### Log levels
Each log message has associated log level, which identifies how important/detailed the message is. NLog can route log messages based primarily on their logger name and log level.

NLog supports the following [log levels](Log-levels):
* `Trace` - very detailed logs, which may include high-volume information such as protocol payloads. This log level is typically only enabled during development
* `Debug` - debugging information, less detailed than trace, typically not enabled in production environment.
* `Info` - information messages, which are normally enabled in production environment
* `Warn` - warning messages, typically for non-critical issues, which can be recovered or which are temporary failures
* `Error` - error messages - most of the time these are `Exceptions`
* `Fatal` - very serious errors!

### Writing log messages
In order to emit log message you can simply call one of the methods on the `Logger`. `Logger` class has six methods whose names correspond to log levels: `Trace()`, `Debug()`, `Info()`, `Warn()`, `Error()` and `Fatal()`. There is also `Log()` method which takes log level as a parameter.
```csharp
using NLog;

public class MyClass
{
  private static Logger logger = LogManager.GetCurrentClassLogger();

  public void MyMethod1()
  {
    logger.Trace("Sample trace message");
    logger.Debug("Sample debug message");
    logger.Info("Sample informational message");
    logger.Warn("Sample warning message");
    logger.Error("Sample error message");
    logger.Fatal("Sample fatal error message");

    // alternatively you can call the Log() method
    // and pass log level as the parameter.
    logger.Log(LogLevel.Info, "Sample informational message");
  }
}
```

Log messages can also be parameterized - you can use the same format strings as when using `Console.WriteLine()` and `String.Format()`:
```csharp
using NLog;

public class MyClass
{
  private static Logger logger = LogManager.GetCurrentClassLogger();

  public void MyMethod1()
  {
    int k = 42;
    int l = 100;

    logger.Trace("Sample trace message, k={0}, l={1}", k, l);
    logger.Debug("Sample debug message, k={0}, l={1}", k, l);
    logger.Info("Sample informational message, k={0}, l={1}", k, l);
    logger.Warn("Sample warning message, k={0}, l={1}", k, l);
    logger.Error("Sample error message, k={0}, l={1}", k, l);
    logger.Fatal("Sample fatal error message, k={0}, l={1}", k, l);
    logger.Log(LogLevel.Info, "Sample informational message, k={0}, l={1}", k, l);
  }
}
```

TIP: You should avoid doing string formatting (such as concatenation, or calling `String.Format()`) yourself and instead use built-in formatting functionality of NLog. The main reason for this is performance:

Formatting log messages takes a lot of time, so NLog tries to defer formatting until it knows that log message will actually be written to some output. If the message ends up being skipped because of logging configuration, you will not pay the price of `String.Format()` at all. See also Optimizing Logging Performance.

## Configuration
So far we have learned how to create log messages from code, but we have not configured any outputs for our logs. So, when you run your instrumented application at this point, you will see - well - nothing. Time to open the NLog.config file and add some logging rules:

1. In the `<targets>` section, add:
```xml
<target name="logfile" xsi:type="File" fileName="file.txt" />
```
This will define a [file target](File-target) which will send logs to a file named file.txt.

2. In the `<rules>` section, add:
```xml
<logger name="*" minlevel="Info" writeTo="logfile" />
```
This snippet will direct all logs (name="\*") of level **Info** or higher (which includes **Info**, **Warn**, **Error** and **Fatal**) to a target named logfile.

Note that as you are typing this in Visual Studio, you should see IntelliSense suggesting attribute names and validating their values. The final configuration should look like this:
```xml
<?xml version="1.0" encoding="utf-8" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

    <targets>
        <target name="logfile" xsi:type="File" fileName="file.txt" />
    </targets>

    <rules>
        <logger name="*" minlevel="Info" writeTo="logfile" />
    </rules>
</nlog>
```
Now, when you run the application, you should see log messages written to file.txt in current directory.

### Multiple targets
Let's try something more complex now. Imagine you want to send very detailed logs to a file, and you also want to see the logs in the console window, but slightly less detailed. Here's the configuration file which implements this:
```xml
<?xml version="1.0" encoding="utf-8" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

    <targets>
        <target name="logfile" xsi:type="File" fileName="file.txt" />
        <target name="console" xsi:type="Console" />
    </targets>

    <rules>
        <logger name="*" minlevel="Trace" writeTo="logfile" />
        <logger name="*" minlevel="Info" writeTo="console" />
    </rules>
</nlog>
```
As you can see, we now have multiple targets and multiple rules which route logs to them.

### Logger-specific routing
Another scenario which is very common requires producing more detailed logs from some components which are being currently developed, while reducing output from some other components. We can use the following configuration:
```xml
<?xml version="1.0" encoding="utf-8" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

    <targets>
        <target name="logfile" xsi:type="File" fileName="file.txt" />
    </targets>

    <rules>
        <logger name="SomeNamespace.Component.*" minlevel="Trace" writeTo="logfile" final="true" />
        <logger name="*" minlevel="Info" writeTo="logfile" />
    </rules>
</nlog>
```
The first rule will send logs from loggers whose names begin with `SomeNamespace.Component`. and where level is `Trace` or higher to the log file. The attribute `final="true"` will cause further processing to be stopped after performing the write.

The second rule will send all remaining logs to the same log file with the restriction that the level must be `Info` or higher.

### Wrappers
NLog supports special kinds of targets which do not do any logging by themselves, but which modify the behavior of other loggers. Those targets are called wrappers. The most commonly used ones are:
* [ImpersonatingWrapper](ImpersonatingWrapper-target) - Impersonates another user for the duration of the write.
* [AsyncWrapper](AsyncWrapper-target) - Provides asynchronous, buffered execution of target writes.
* [FallbackGroup](FallbackGroup-target) - Provides fallback-on-error.
* [FilteringWrapper](FilteringWrapper-target) - Filters log entries based on a condition.

Many more wrappers are available. You can find the full list [here](Targets).

In order to use wrappers, simply enclose the `<target />` element with another one representing a wrapper and use the name of the wrapper in your `<rules/>` section as in the following example:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

    <targets>
        <target name="asyncFile" xsi:type="AsyncWrapper">
            <target name="logfile" xsi:type="File" fileName="file.txt" />
        </target>
    </targets>

    <rules>
        <logger name="*" minlevel="Info" writeTo="asyncFile" />
    </rules>
</nlog>
```
This will make all writes to the file be asynchronous, which will improve responsiveness of the calling thread.

### Layouts
Layouts provide a way to format the contents of the logs as it is written to a file. There are 2 main kinds of layouts:
* simple layout - which is composed of [Layout Renderers](Layout-renderers)
* structural layouts - which can output XML, CSV, and other complex formats

Simple layout is just a string, with special tags embedded between **${** and **}**. For example the following declaration will cause each log message to be prefixed with date formatted as **yyyyMMddHHmmss**:
```xml
<target name="logfile" xsi:type="File" fileName="file.txt" layout="${date:format=yyyyMMddHHmmss} ${message}" />
```


## Advanced

### Expose logger to sub-classes
When we wish to expose the logger into sub classes the following pattern could be used.

```csharp
class BaseClass
{
    protected BaseClass()
    {
        Log = LogManager.GetLogger(GetType().FullName);
    }

    protected Logger Log { get; private set; }
}

class ExactClass : BaseClass
{
    public ExactClass() : base() { }
    ...
}
```

The `LogManager.GetLogger()` method should NOT be invoked in the constructor of the BaseClass with Type parameter argument i.e. 

``` C#
protected BaseClass()
{
    Log = LogManager.GetLogger(GetType().FullName, GetType());
}
```

as an exception will be thrown.

In case of the ExactClass has a default constructor which invokes the BaseClass constructor a ```System.StackOverflowException``` is thrown. This is because the ExactClass calls the BaseClass the GetLogger(String, Type) attempts to construct a ExactClass until the exception is thrown.

```
ExactClass => BaseClass => ExactClass => BaseClass => ...
```

When there is no default constructor at the ExactClass the GetLogger(String, Type) method call does not know how to construct the ExactClass and it fails with a ```NLog.NLogConfigurationException```.