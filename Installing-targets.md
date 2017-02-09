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
            NOTE: call LogManager.Configuration.Install(new InstallationContext()); To execute this query.
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