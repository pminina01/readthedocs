A specialized layout that renders Log4j-compatible XML events. 

Supported in .NET, Silverlight, Compact Framework and Mono

## Configuration Syntax
```xml
<targets>
  <target>
    <layout xsi:type="Log4JXmlEventLayout">
    </layout>
  </target>
</targets>
```

## Parameters
* **includeMdc** - Indicates whether to include contents of the [[MappedDiagnosticsContext|MDC-Layout-Renderer]] dictionary. Boolean
  > Introduced in NLog 4.4.9
* **includeNdc** - Indicates whether to include contents of the [[MappedDiagnosticsContext|NDC-Layout-Renderer]] stack. Boolean
  > Introduced in NLog 4.5
* **includeMdlc** - Indicates whether to include contents of the async [[MappedDiagnosticsLogicalContext|MDLC-Layout-Renderer]] dictionary. Boolean
  > Introduced in NLog 4.4.9. .NET 4.0 or 4.5 required.
* **includeNdlc** - Indicates whether to include contents of the async [[NestedDiagnosticsLogicalContext|NDLC-Layout-Renderer]] stack. Boolean
  > Introduced in NLog 4.5
* **includeAllProperties** - Indicates whether to include contents of all the log-event properties. Boolean
  > Introduced in NLog 4.4.9

## Remarks
This layout is not meant to be used explicitly. Instead you can use ${log4jxmlevent} layout renderer.