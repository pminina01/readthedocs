XML event description compatible with log4j, Chainsaw and NLogViewer. 

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${log4jxmlevent:ndcItemSeparator=String:includeSourceInfo=Boolean:includeCallSite=Boolean
               :includeMdc=Boolean:appInfo=String:includeNdc=Boolean
               :indentXml=Boolean:includeNLogData=Boolean}
```

##Parameters
###Payload Options
* **ndcItemSeparator** - NDC item separator. Default:

  > This parameter is not supported in:
  > * NLog v1.0 for .NET Compact Framework 1.0
  > * NLog v1.0 for .NET Compact Framework 2.0
  > * NLog v1.0 for .NET Framework 1.0
  > * NLog v1.0 for .NET Framework 1.1
  > * NLog v1.0 for .NET Framework 2.0

* **includeSourceInfo** - Indicates whether to include source info (file name and line number) in the information sent over the network. Boolean
  > This parameter is not supported in:
  > * NLog v1.0 for .NET Compact Framework 1.0
  > * NLog v1.0 for .NET Compact Framework 2.0
  > * NLog v2.0 for .NET Compact Framework 2.0
  > * NLog v2.0 for .NET Compact Framework 3.5

* **includeCallSite** - Indicates whether to include call site (class and method name) in the information sent over the network. Boolean
  > This parameter is not supported in:
  > * NLog v1.0 for .NET Compact Framework 1.0
  > * NLog v1.0 for .NET Compact Framework 2.0
  > * NLog v2.0 for .NET Compact Framework 2.0
  > * NLog v2.0 for .NET Compact Framework 3.5

* **includeMdc** - Indicates whether to include contents of the MappedDiagnosticsContext dictionary. Boolean
* **appInfo** - AppInfo field. By default it's the friendly name of the current AppDomain.
* **includeNdc** - Indicates whether to include contents of the NestedDiagnosticsContext stack. Boolean
* **indentXml** - Indicates whether the XML should use spaces for indentation. Boolean
* **includeNLogData** - Indicates whether to include NLog-specific extensions to log4j schema. Boolean Default: True