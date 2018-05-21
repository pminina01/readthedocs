Globally-unique identifier (GUID). 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${guid:format=String}
```

## Parameters
### Rendering Options
* **format** - GUID format as accepted by Guid.ToString() method. Default: `N`
* **GeneratedFromLogEvent** - Creates a special GUID from the LogEvent, so if the LogEvent is written to multiple targets, then all targets will get the same GUID for the LogEvent (Like a CorrelationId). Default: `False`