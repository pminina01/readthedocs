It uses [Mapped Diagnostic Logical Context] (Mapped-Diagnostic-Logical-Context).

As of NLog 4.1 in the NLog assembly.

Supported in .NET 4.0 and 4.5.

##Configuration Syntax
```
${mdlc:item=String}
```

##Parameters
###Rendering Options
* **item** - Name of the item. Required.

##Example
###Simple Properties
The following example demonstrates the basic usage of the Mapped Diagnostic Logical Context.

```c#
MappedDiagnosticsLogicalContext.Set("PropertyName", "PropertyValue");
MappedDiagnosticsLogicalContext.Set("PropertyName2", "AnotherPropertyValue");
```

Add the following to your logger configuration to reference the above properties.
```xml
${mdlc:item=PropertyName}
${mdlc:item=PropertyName2}
```
