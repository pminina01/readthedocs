The time in a 24-hour, sortable format HH:mm:ss.mmm. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${time:universalTime=Boolean:invariant=Boolean}
```

## Parameters
### Rendering Options
* **universalTime** - Indicates whether to output UTC time instead of local time. Boolean Default: False
* **invariant** - Indicates whether to output in invariant time format, and not lookup of current cultureinfo. Boolean Default: False
  > Introduced with NLog 4.5.2