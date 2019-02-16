Some targets support installing. Current the following targets support installing

- Database target
- EventLogger target
- PerformanceCounter target

## Install

Install all targets used in the config:

```c#
LogManager.Configuration.Install(new InstallationContext());
```

## Uninstall

Uninstall all targets used in the config:

```C#
LogManager.Configuration.Uninstall(new InstallationContext());
```

# Example install database target

```xml
<target xsi:type="Database" name="db"
        connectionStringName="LoggingDatabase">
    <install-command>
        <text>
            <!--
            NOTE: call LogManager.Configuration.Install(new InstallationContext()); 
                  to execute this query.
            -->
            CREATE TABLE ${var:logTableName} (
            Id bigint primary key not null identity(1,1),
            Logged datetime2,
            Level nvarchar(10),
            LogMessage nvarchar(max),
            MessageUid uniqueidentifier,
            MessagePartUid uniqueidentifier,
            MessagePartDataUid uniqueidentifier,
            )
        </text>
        <ignoreFailures>false</ignoreFailures>
    </install-command>
```


# Troubleshooting installation issues

## Installation log

You can enable the installation log by overriding the default output stream in your `InstallationContext`. For example, to have the installation log printed out to console, you can use:

```csharp
LogManager.Configuration.Install(new InstallationContext(Console.Out));
```

You can also redirect the installation log to a string in memory:

```csharp
var stringWriter = new StringWriter();
LogManager.Configuration.Install(new InstallationContext(stringWriter));
var installationLog = stringWriter.ToString();   // retrieve the installation output
```

Note that the log output can also be accessed via `InstallationContext.LogOutput`:

```csharp
// This is equivalent to the previous example
var installationContext = new InstallationContext(new StringWriter())
LogManager.Configuration.Install(installationContext);
var installationLog = installationContext.LogOutput.ToString();
```

## A note on exceptions

Except for application critical exceptions (OutOfMemoryException. StackOverflowException and ThreadAbortException), `LogManager.Configuration.Install()` will not rethrow any other exception, even when NLog is [[set up to throw exceptions | Logging-troubleshooting#troubleshooting-steps]]. You can set up NLog to use a [[fallback target | FallbackGroup-target]] if your primary target (for instance a log database) fails.
