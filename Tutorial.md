##Installing NLog
NLog can be downloaded from the the [Download](http://nlog-project.org/download.html) section or from [NuGet](http://nuget.org). Both source and binary packages are available. For beginners, it is a good idea to use the recommended installer package in msi or exe format. More advanced scenarios may require the use of zip files, which are also available.

At this time NLog 2.0 is stable and can be tried for production applications.

Once you have downloaded the installation package, run it and choose default installation options. This will deploy NLog assemblies, API documentation and Visual Studio integration, which includes:

* Item Templates - to quickly add NLog [Configuration File](Configuration-file) to your project
* Code Snippets - for C# and Visual Basic, to simplify creation of Logger instances
* NLog.xsd file Intellisense(tm) support for editing NLog configuration files registration of NLog binary directory into **Add Reference...** dialog

##Adding NLog to an application
Let's start by creating an empty console project in Visual Studio.

In order to use NLog in the application, we must add a reference to NLog.dll and a [Configuration File](Configuration-file) which will specify Log Routing rules. Those two things can be done in a single step, just by adding NLog.config file to the project. To do so, right click on your project in Visual Studio and select **Add New Item**.

From the list on the left, select **NLog** category, then select **Empty NLog Configuration File** then click **Add**.

[[File-AddNewItem.png]]

This will add a reference to NLog.dll from C:\Program Files\NLog and a [Configuration File](Configuration-file) without any rules. Since NLog requires the configuration file to be copied to the application directory, we must make just one change. In Solution Explorer select NLog.config and set **Copy to output** directory to **Copy always**.

[[CopyToOutputDirectory.png]]

That's it, you can now compile and run your application and it will be able to use NLog.

##Logging API
In order to emit log messages from the application you need to use the logging API. There are two classes that you will be using the most: Logger and LogManager, both in the NLog namespace. Logger represents the named source of logs and has methods to emit log messages, and LogManager creates and manages instances of loggers.

It is important to understand that Logger does not represent any particular log output (and thus is never tied to a particular log file, etc.) but is only a source, which typically corresponds to a class in your code. Mapping from log sources to outputs is defined separately through [Configuration File](Configuration-file) or [Configuration API](Configuration-API). Maintaining this separation lets you keep logging statements in your code and easily change how and where the logs are written, just by updating the configuration in one place.

##Creating loggers
Most applications will use one logger per class, where the name of the logger is the same as the name of the class. As mentioned before, you must use LogManager to create Logger instances. To create a logger with a given name, call:
```csharp
using NLog;
 
Logger logger = LogManager.GetLogger("MyClassName");
```

In most cases you will have one logger per class, so it makes sense to give logger the same name as the current class. `LogManager` exposes a method which creates a logger for current class, called `GetCurrentClassLogger()`. Because loggers are thread-safe, you can simply create the logger once and store it in a static variable:
```csharp
namespace MyNamespace
{
  public class MyClass
  {
    private static Logger logger = LogManager.GetCurrentClassLogger();
  }
}
```

TIP: Instead of writing logger declaration by hand, you can use Visual Studio code snippet: Just type nlogger and press TAB key twice, which will insert the snippet.

##Log levels
Each log message has associated log level, which identifies how important/detailed the message is. NLog can route log messages based primarily on their logger name and log level.

NLog supports the following [log levels](Log-levels):
* Trace - very detailed logs, which may include high-volume information such as protocol payloads. This log level is typically only enabled during development
* Debug - debugging information, less detailed than trace, typically not enabled in production environment.
* Info - information messages, which are normally enabled in production environment
* Warn - warning messages, typically for non-critical issues, which can be recovered or which are temporary failures
* Error - error messages
* Fatal - very serious errors

##Emitting log messages
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
    logger.Log(LogLevel.Info, "Sample fatal error message");
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
    logger.Log(LogLevel.Info, "Sample fatal error message, k={0}, l={1}", k, l);
  }
}
```

TIP: You should avoiding doing string formatting (such as concatenation, or calling String.Format) yourself and instead use built-in formatting functionality of NLog. The main reason for this is performance:

Formatting log messages takes a lot of time, so NLog tries to defer formatting until it knows that log message will actually be written to some output. If the message ends up being skipped because of logging configuration, you will not pay the price of `String.Format()` at all. See also Optimizing Logging Performance.

##Configuration File
So far we have learned how to emit log messages from code, but we have not configured any outputs for out logs. So, when you run your instrumented application at this point, you will see - well - nothing. Time to open the NLog.config file and add some logging rules:

1. In the \<targets> section, add:
```
<target name="logfile" xsi:type="File" fileName="file.txt" />
```
This will define a target which will send logs to a file named file.txt.

2. In the \<rules> section, add:
```
<logger name="*" minlevel="Info" writeTo="logfile" />
```
This snippet will direct all logs (name="*") of level **Info** or higher (which includes **Info**, **Warn**, **Error** and **Fatal**) to a target named logfile.

Note that as you are typing this in Visual Studio, you should see Intellisense suggesting attribute names and validating their values. The final configuration should look like this:
```
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

##Multiple targets
Lets try something more complex now. Imagine you want to send very detailed logs to a file, and you also want to see the logs in the console window, but slighly less detailed. Here's the configuration file which implements this:
```
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

##Logger-specific routing
Another scnenario which is very common requires producing more detailed logs from some components which are being currently developed, while reducing output from some other components. We can use the following configuration:
```
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
First rule will send logs from loggers whose names begin with `SomeNamespace.Component`. and where level is **Trace** or higher to the log file. The attribute _final="true"_ will cause further processing to be stopped after performing the write.

Second rule will send all remaining logs to the same log file with the restriction that the level must be **Info** or higher.

##Wrappers
NLog supports a special kind of targets, which don't do any logging by themselves, but which modify the behavior of other loggers. Those targets are called wrappers. The most commonly used ones are:
* [ImpersonatingWrapper](ImpersonatingWrapper-target) - Impersonates another user for the duration of the write.
* [AsyncWrapper](AsyncWrapper-target) - Provides asynchronous, buffered execution of target writes.
* [FallbackGroup](FallbackGroup-target) - Provides fallback-on-error.
* [FilteringWrapper](FilteringWrapper-target) - Filters log entries based on a condition.

Many more wrappers are available. You can find the full list [here](Targets).

In order to use wrappers, simply enclose the \<target /> element with another one representing a wrapper and use the name of the wrapper in your \<rules/> section as in the following example:

```
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

##Layouts
Layouts provide a way to format the contents of the logs as it is written to a file. There are 2 main kinds of layouts:
* simple layout - which is composed of [Layout Renderers](Layout-renderers)
* structural layouts - which can output XML, CSV, and other complex formats

Simple layout is just a string, with special tags embedded between **${** and **}**. For example the following declaration will cause each log message to be prefixed with date formatted as **yyyyMMddHHmmss**:
```
<target name="logfile" xsi:type="File" fileName="file.txt" layout="${date:format=yyyyMMddHHmmss} ${message}" />
```