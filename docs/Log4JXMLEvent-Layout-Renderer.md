XML event description compatible with log4j, Chainsaw and NLogViewer. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${log4jxmlevent:ndcItemSeparator=String:includeSourceInfo=Boolean:includeCallSite=Boolean
               :includeMdc=Boolean:includeMdlc=Boolean:appInfo=String:includeNdc=Boolean
               :indentXml=Boolean:includeAllProperties=Boolean:includeNLogData=Boolean}
```

## Parameters
### Payload Options
* **appInfo** - AppInfo field. By default it's the friendly name of the current AppDomain.

* **loggerName** - Logger field. By default it's the output of `${logger}`
  > Introduced in NLog 4.5

* **includeSourceInfo** - Indicates whether to include source info (file name and line number) in the information sent over the network. Boolean

* **includeCallSite** - Indicates whether to include call site (class and method name) in the information sent over the network. Boolean

* **includeMdc** - Indicates whether to include contents of the [[MappedDiagnosticsContext|MDC-Layout-Renderer]] dictionary. Boolean

* **includeMdlc** - Indicates whether to include contents of the async [[MappedDiagnosticsLogicalContext|MDLC-Layout-Renderer]] dictionary (Thread Context Map). Boolean
  > Introduced in NLog 4.4.8 (.NET 4.0 or 4.5 required)

* **includeAllProperties** - Indicates whether to include contents of all the log-event properties. Boolean
  > Introduced in NLog 4.4.9

* **includeNdc** - Indicates whether to include contents of the [[NestedDiagnosticsContext|NDC-Layout-Renderer]] stack. Boolean
* **ndcItemSeparator** - NDC item separator. Default: 

* **includeNdlc** - Indicates whether to include contents of the [[NestedDiagnosticsLogicalContext|NDLC-Layout-Renderer]] stack. Boolean
  > Introduced in NLog 4.5
* **ndlcItemSeparator** - NDLC item separator. Default: 
  > Introduced in NLog 4.5

* **indentXml** - Indicates whether the XML should use spaces for indentation. Boolean

* **includeNLogData** - Indicates whether to include NLog-specific extensions to log4j schema. Boolean Default: True