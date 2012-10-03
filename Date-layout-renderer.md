Current date and time. 

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${date:universalTime=Boolean:format=String:culture=Culture}
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

* **format** - Date format. Can be any argument accepted by DateTime.ToString(format).
* **culture** - Culture used for rendering.Culture