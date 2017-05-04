XML event description compatible with log4j, Chainsaw and NLogViewer. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${log4jxmlevent:ndcItemSeparator=String:includeSourceInfo=Boolean:includeCallSite=Boolean
               :includeMdc=Boolean:includeMdlc=Boolean:appInfo=String:includeNdc=Boolean
               :indentXml=Boolean:IncludeAllProperties=Boolean:includeNLogData=Boolean}
```

## Parameters
### Payload Options
* **includeSourceInfo** - Indicates whether to include source info (file name and line number) in the information sent over the network. Boolean

* **includeCallSite** - Indicates whether to include call site (class and method name) in the information sent over the network. Boolean

* **includeMdc** - Indicates whether to include contents of the MappedDiagnosticsContext dictionary. Boolean
* **includeMdlc** - Indicates whether to include contents of the MappedDiagnosticsLogicalContext dictionary. Boolean
  > Introduced in NLog 4.4.8. .NET 4.0 or 4.5 required.
* **IncludeAllProperties** - Indicates whether to include contents of all the log-event properties. Boolean
  > Introduced in NLog 4.4.9

* **appInfo** - AppInfo field. By default it's the friendly name of the current AppDomain.
* **includeNdc** - Indicates whether to include contents of the NestedDiagnosticsContext stack. Boolean
* **ndcItemSeparator** - NDC item separator. Default: 
* **indentXml** - Indicates whether the XML should use spaces for indentation. Boolean
* **includeNLogData** - Indicates whether to include NLog-specific extensions to log4j schema. Boolean Default: True