## Content
* [[Installing NLog|tutorial#installing-nlog]]
* [[Configure NLog Targets for output|tutorial#configure-nlog-targets-for-output]]
* [[Writing log messages|tutorial#writing-log-messages]]
* * [[Log levels|tutorial#log-levels]]
* * [[Layouts and LayoutRenderers|tutorial#layouts-and-layoutrenderers]]
* [[Multiple targets|tutorial#multiple-targets]]
* [[Logger-specific routing|tutorial#logger-specific-routing]]
* [[Wrappers|tutorial#wrappers]]
* [[Advanced|tutorial#advanced]]

## Installing NLog

> ASP.NET Core users should follow [Getting started with ASP.NET Core](https://github.com/NLog/NLog.Web/wiki/Getting-started-with-ASP.NET-Core-(csproj---vs2017)) first.

[NLog](https://www.nuget.org/packages/NLog/) can be downloaded from NuGet.

Just install [NLog.Config package](https://www.nuget.org/packages/NLog.Config/) and this will install also [NLog](https://www.nuget.org/packages/NLog) and [NLog.Schema](https://www.nuget.org/packages/NLog.Schema) packages - this will result in a starter config and intellisense.



Use the GUI or the following command in the Package Manager Console:
```
Install-Package NLog.Config
```

That's it, you can now compile and run your application and it will be able to use NLog.

## Configure NLog Targets for output
NLog will only produce output if having configured one (or more) NLog targets.

To configure using XML, then add a `NLog.config` file to your application project (File Properties: Copy Always). This is a very simple example of a `NLog.config`:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

    <targets>
        <target name="logfile" xsi:type="File" fileName="file.txt" />
        <target name="logconsole" xsi:type="Console" />
    </targets>

    <rules>
        <logger name="*" minlevel="Info" writeTo="logconsole" />
        <logger name="*" minlevel="Debug" writeTo="logfile" />
    </rules>
</nlog>
```

To configure programmatically, then one can do this in code:

```csharp
var config = new NLog.Config.LoggingConfiguration();

var logfile = new NLog.Targets.FileTarget() { FileName = "file.txt", Name = "logfile" };
var logconsole = new NLog.Targets.ConsoleTarget() { Name = "logconsole" };

config.LoggingRules.Add(new NLog.Config.LoggingRule("*", LogLevel.Info, logconsole));
config.LoggingRules.Add(new NLog.Config.LoggingRule("*", LogLevel.Debug, logfile));

NLog.LogManager.Configuration = config;
```

See also [Configuration File](Configuration-file) or [Configuration API](Configuration-API)

## Writing log messages
Example of how to acquire a logger and writing a message to the logger:

```csharp
var logger = NLog.LogManager.GetCurrentClassLogger();
logger.Info("Hello World");
```

If having configured the NLog targets correctly, then it will output the message to the configured targets.

The logger has a name, which is used by the logging-rules (See `name="*"` in configuration example above) to redirect to the wanted targets.

When using `NLog.LogManager.GetCurrentClassLogger()`, then it will create a logger with the name of the calling class (with namespace). One can also specify an explicit name by using `NLog.LogManager.GetLogger("MyLogger")`.

The logger can write messages with different LogLevels, which is used by the logging-rules (See `minLevel` in configuration example above) so only relevant messages are redirected to the wanted targets:

The logger is not tied to a specific target. The messages written to one logger can reach multiple targets based on the logging-rules configuration. Maintaining this separation lets you keep logging statements in your code and easily change how and where the logs are written, just by updating the configuration in one place.

### Log levels
Each log message has associated log level, which identifies how important/detailed the message is. NLog can route log messages based primarily on their logger name and log level.

NLog supports the following [log levels](Log-levels):
* `Trace` - very detailed logs, which may include high-volume information such as protocol payloads. This log level is typically only enabled during development
* `Debug` - debugging information, less detailed than trace, typically not enabled in production environment.
* `Info` - information messages, which are normally enabled in production environment
* `Warn` - warning messages, typically for non-critical issues, which can be recovered or which are temporary failures
* `Error` - error messages - most of the time these are `Exceptions`
* `Fatal` - very serious errors!

```csharp
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

### Layouts and LayoutRenderers
It is possible to configure how log messages are written to a NLog target.

This shows the default `SimpleLayout` used by most NLog targets:

```xml
<target name="logfile" xsi:type="File" fileName="file.txt" layout="${longdate}|${level:uppercase=true}|${logger}|${message}" />
```

This can be configured to include much details:

```xml
<target name="logfile" xsi:type="File" fileName="file.txt" layout="${longdate}|${level:uppercase=true}|${logger}|${threadid}|${message}|{exception:format=tostring}" />
```

See full list here: [Layout Renderers](Layout-Renderers)

One can also use a more complex Layout instead of `SimpleLayout`:
* [[CsvLayout]]
* [[JsonLayout]]

See full list here: [[Layouts]]

### Best Practises for Logging

#### 1. Logger should be a static variable in each class
Creating a new Logger has an overhead, as it has to acquire locks and allocate objects.

Therefore it is advise to create the logger like this:

```csharp
namespace MyNamespace
{
  public class MyClass
  {
    private static Logger logger = NLog.LogManager.GetCurrentClassLogger();
  }
}
```

#### 2. Logger should handle string formatting
Avoid performing string allocation or string concatenation upfront, but instead let the Logger do the formatting. This will allow NLog to defer the formatting and reduce overhead.

Therefore it is advise to perform the logging like this:
```csharp
logger.Info("Hello {0}", "Earth");
```

## Wrappers
NLog supports special kinds of targets which do not do any logging by themselves, but which modify the behavior of other loggers. Those targets are called wrappers. The most commonly used ones are:
* [AsyncWrapper](AsyncWrapper-target) - Provides asynchronous, buffered execution of target writes.
* [FallbackGroup](FallbackGroup-target) - Provides fallback-on-error.
* [RetryingWrapper](RetryingWrapper-target) - Provides retry-on-error.

See full list here: (Target Wrappers)[Targets#wrappers]

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