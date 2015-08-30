It uses [Mapped Diagnostic Logical Context] (Mapped-Diagnostic-Logical-Context).
 
As of NLog 4.1, the Mapped Diagnostic Logical Context supports just `String`.

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

###Dynamic Properties
The following example demonstrates a Mapped Diagnostic Logical Context property that renders the value of `Environment.TickCount` at the time that the context item is rendered.

```c#
public class MdcTickProperty 
{
   public static readonly MdcTickProperty Default = new MdcTickProperty();

   private MdcTickProperty () 
   {
   }

   public override string ToString () 
   {
      return Environment.TickCount.ToString();
   }
}
```

Add the `MdcTickProperty` instance to the Mapped Diagnostic Logical Context. This will affect the current logical context, as the Mapped Diagnostic Logical Context is logical context.

```c#
MappedDiagnosticsLogicalContext.Set("TickCount", MdcTickProperty.Default.ToString());
```

In the logging configuration, include:

```xml
${mdc:item=TickCount}
```