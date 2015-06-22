Global Diagnostics Context - a dictionary structure to hold per-application-instance values.

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${gdc:item=String}
```

##Parameters
###Rendering Options
* **item** - Name of the item. Required.

##API
Set a value in the GDC

```c#
GlobalDiagnosticsContext.Set("myDataBase","someValue");
```