Value from the appsettings.json or other configuration in .NET Core

Introduced NLog.Extensions.Logging 1.3 and NLog.Web.AspNetCore 4.7

---
 ℹ️  For .NET Core 2.1 Console application you need install the `NLog.Extensions.Configuration` package and include it
to `<extensions>` tag in `nlog.config`

---

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