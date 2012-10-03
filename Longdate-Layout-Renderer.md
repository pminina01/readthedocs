The date and time in a long, sortable format yyyy-MM-dd HH:mm:ss.mmm. 

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${longdate:universalTime=Boolean}
```

##Parameters
###Rendering Options
* **universalTime** - Indicates whether to output UTC time instead of local time.Boolean Default: False

  > This parameter is not supported in:
  > * NLog v1.0 for .NET Compact Framework 1.0
  > * NLog v1.0 for .NET Compact Framework 2.0
  > * NLog v1.0 for .NET Framework 1.0
  > * NLog v1.0 for .NET Framework 1.1
  > * NLog v1.0 for .NET Framework 2.0