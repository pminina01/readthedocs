Current date and time. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${date:universalTime=Boolean:format=String:culture=Culture}
```

## Parameters
### Rendering Options
* _universalTime_ - Indicates whether to output UTC time instead of local time.Boolean Default: False
* _format_ - Date format. Can be any argument accepted by DateTime.ToString(format). Note that colons needs to escaped with a backslash. Example: `${date:format=yyyy-MM-dd HH\:mm\:ss.fff}`
* _culture_ - Culture used for rendering.Culture