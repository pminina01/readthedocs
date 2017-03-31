Current date and time. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${date:universalTime=Boolean:format=String:culture=Culture}
```

## Parameters
### Rendering Options
* **universalTime** - Indicates whether to output UTC time instead of local time.Boolean Default: False
* **format** - Date format. Can be any argument accepted by DateTime.ToString(format). Note that colons need to escaped with a backslash. Example: `${date:format=yyyy-MM-dd HH\:mm\:ss.fff}`
* **culture** - Culture used for rendering.Culture