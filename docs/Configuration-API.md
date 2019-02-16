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

class Example
{
    static void Main(string[] args)
    {
        // Step 1. Create configuration object 
        var config = new LoggingConfiguration();

        // Step 2. Create targets
        var consoleTarget = new ColoredConsoleTarget("target1")
        {
            Layout = @"${date:format=HH\:mm\:ss} ${level} ${message} ${exception}"
        };
        config.AddTarget(consoleTarget);

        var fileTarget = new FileTarget("target2")
        {
            FileName = "${basedir}/file.txt",
            Layout = "${longdate} ${level} ${message}  ${exception}"
        };
        config.AddTarget(fileTarget);


        // Step 3. Define rules
        config.AddRuleForOneLevel(LogLevel.Error, fileTarget); // only errors to file
        config.AddRuleForAllLevels(consoleTarget); // all to console

        // Step 4. Activate the configuration
        LogManager.Configuration = config;

        // Example usage
        Logger logger = LogManager.GetLogger("Example");
        logger.Trace("trace log message");
        logger.Debug("debug log message");
        logger.Info("info log message");
        logger.Warn("warn log message");
        logger.Error("error log message");
        logger.Fatal("fatal log message");

        //Example of logging exceptions

        try
        {

        }
        catch (Exception ex)
        {
            logger.Error(ex, "ow noos!");
            throw;
        }
    }
}
```

### Passing Custom Values
Another simple example of additional functionality in code is the use of the [${event-properties}](EventProperties-Layout-Renderer) layout renderer.