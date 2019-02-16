Combining XML config with C# config is tricky, as autoreload/load of the XML file could overwrite the C# config.

To combine both, the `ConfigurationReloaded` event is needed

## Example

- We use the nlog.config and
- We add the console target and rules in C#

```c#
using System;
using NLog;
using NLog.Config;
using NLog.Targets;

class Program
{
    // Define a static logger variable so that it references the logger instanced named "Scribe"
    private static readonly Logger log = LogManager.GetCurrentClassLogger();

    static void Main(string[] args)
    {
        ExtendNLogConfig();

        LogManager.ConfigurationReloaded += LogManager_ConfigurationReloaded;

        log.Info("Entering Application.");

        Console.WriteLine("Press any key to exit ...");
        Console.Read();
    }


    private static void LogManager_ConfigurationReloaded(object sender, LoggingConfigurationReloadedEventArgs e)
    {
        ExtendNLogConfig();
    }

    /// <summary>
    /// Extend the logging rules in the nlog.config with programmically rules.
    /// </summary>
    private static void ExtendNLogConfig()
    {
        //don't set  LogManager.Configuration because that will overwrite the nlog.config settings
        var consoleTarget = new ColoredConsoleTarget();
        consoleTarget.Name = "console";
        LogManager.Configuration.AddTarget("console", consoleTarget);

        consoleTarget.Layout = @"${date:format=HH\:mm\:ss} ${logger} ${message} ${exception} ${event-context:item=MyValue}";
        var rule1 = new LoggingRule("*", LogLevel.Debug, consoleTarget);
        LogManager.Configuration.LoggingRules.Add(rule1);
        LogManager.ReconfigExistingLoggers();
    }
}

```