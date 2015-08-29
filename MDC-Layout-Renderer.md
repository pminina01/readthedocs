Mapped Diagnostics Context - a thread-local structure that keeps a dictionary
of strings and provides methods to output them in layouts. 

Use the Mapped Diagnostics Context when you have information that you want available to every logger executing on the current thread. As the Mapped Diagnostics Context is thread-local, you must configure all properties within the context of each thread where the property value is required.

When you need the context for all threads, use the [GDC](https://github.com/NLog/NLog/wiki/Gdc-Layout-Renderer). If the context is different for every message, use the [Log event properties](https://github.com/NLog/NLog/wiki/EventProperties-Layout-Renderer). 
 
As of NLog 4.1, the Mapped Diagnostics Context supports any `Object` type, not just `String`.

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${mdc:item=String}
```

##Parameters
###Rendering Options
* **item** - Name of the item. Required.

##Example
###Simple Properties
The following example demonstrates the basic usage of the Mapped Diagnostics Context.

```c#
MappedDiagnosticsContext.Set("PropertyName", "PropertyValue");
MappedDiagnosticsContext.Set("Property2", new { Part1 = 2.0m, Part2 = "Two parts" });
MappedDiagnosticsContext.Set("Property3", AnyObjectOrString);
```

Add the following to your logger configuration to reference the above properties.
```xml
${mdc:item=PropertyName}
${mdc:item=Property2}
${mdc:item=Property3}
```

###Dynamic Properties
The following example demonstrates a Mapped Diagnostics Context property that renders the value of `Environment.TickCount` at the time that the context item is rendered.

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

Add the `MdcTickProperty` instance to the Mapped Diagnostics Context. This will only affect the current thread, as the Mapped Diagnostics Context is thread-local.

```c#
MappedDiagnosticsContext.Set("TickCount", MdcTickProperty.Default);
```

In the logging configuration, include:

```xml
${mdc:item=TickCount}
```

##Notes
When rendering context items, the item is passed to `String.Format` along with the current configuration's `DefaultCultureInfo` value.