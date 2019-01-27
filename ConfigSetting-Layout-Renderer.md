Value from the appsettings.json or other configuration in .NET Core

> Introduced NLog.Extensions.Logging 1.4.0 and NLog.Web.AspNetCore 4.8.0

## Register Configuration
When calling `UseNLog()` from `NLog.Web.AspNetCore` or `NLog.Extensions.Hosting` then it will automatically register hosting environment configuration with `ConfigSettingLayoutRenderer`.

To manual register the Microsoft Extension `IConfiguration` with `${configsetting}`:

```c#
IConfigurationRoot config = new ConfigurationBuilder()
    .AddJsonFile(path: "AppSettings.json").Build();
NLog.Extensions.Logging.ConfigSettingLayoutRenderer.DefaultConfiguration = config;
```

## Configuration Syntax
```
${configsetting:name=String:default=String}
```

## Parameters

### Rendering Options

* **name** - Key in the config. Required. Use `.` for nested objects.
* **Default** - Default value if not present. Optional.

## Example

Example: appsettings.json:

```json
{
    "Mode":"Prod",
    "Options":{
        "StorageConnectionString":"UseDevelopmentStorage=true",
    }
}
```


Config Setting Lookup:

```
${configsetting:name=Mode} // renders "Prod"
${configsetting:name=Options.StorageConnectionString} // renders "UseDevelopmentStorage=true"
${configsetting:name=Options.TableName:default=MyTable} // renders "MyTable"
```   

Config Setting Lookup Cached:

```
${configsetting:cached=True:name=Mode}
```