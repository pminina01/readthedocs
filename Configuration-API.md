NLog can be also configured programmatically.

## Use
In order to configure NLog in code you must complete the following steps:
 1. Create a `LoggingConfiguration` object that will hold the configuration
 2. Create one or more targets (objects of classes inheriting from `Target`)
 3. Set the properties of the targets
 4. Define logging rules through `LoggingRule` objects and add them to the configuration's `LoggingRules`
 5. Activate the configuration by assigning the configuration object to `LogManager.Configuration`

## Examples
### Multiple targets
This sample demonstrates the programmatic creation of two targets: one is a colored console, and the other is a file and rules that send messages to them for messages whose level is `Debug` or higher.
```c#
using NLog;
using NLog.Targets;
using NLog.Config;
using NLog.Win32.Targets;

class Example
{
    static void Main(string[] args)
    {
        // Step 1. Create configuration object 
        var config = new LoggingConfiguration();

        // Step 2. Create targets and add them to the configuration 
        var consoleTarget = new ColoredConsoleTarget();
        config.AddTarget("console", consoleTarget);

        var fileTarget = new FileTarget();
        config.AddTarget("file", fileTarget);

        // Step 3. Set target properties 
        consoleTarget.Layout = @"${date:format=HH\:mm\:ss} ${logger} ${message}";
        fileTarget.FileName = "${basedir}/file.txt";
        fileTarget.Layout = "${message}";

        // Step 4. Define rules
        var rule1 = new LoggingRule("*", LogLevel.Debug, consoleTarget);
        config.LoggingRules.Add(rule1);

        var rule2 = new LoggingRule("*", LogLevel.Debug, fileTarget);
        config.LoggingRules.Add(rule2);

        // Step 5. Activate the configuration
        LogManager.Configuration = config;

        // Example usage
        Logger logger = LogManager.GetLogger("Example");
        logger.Trace("trace log message");
        logger.Debug("debug log message");
        logger.Info("info log message");
        logger.Warn("warn log message");
        logger.Error("error log message");
        logger.Fatal("fatal log message");
    }
}
```

### Passing Custom Values
Another simple example of additional functionality in code is the use of the [${event-context}](Event-Context-Layout-Renderer) layout renderer.