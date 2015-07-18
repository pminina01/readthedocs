Mapped Diagnostics Context - a thread-local structure that keeps a dictionary
of strings and provides methods to output them in layouts. 

Use the Mapped Diagnostics Context when you have information that you want available to every logger executing on the current thread. As the Mapped Diagnostics Context is thread-local, you must configure all properties within the context of each thread where the property value is required.
 
As of NLog 4.0.1, the Mapped Diagnostics Context supports any `Object` type, not just `String`.

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${mdc:item=String}
```

##Parameters
###Rendering Options
* **item** - Name of the item. Required.

##Example
The following example demonstrates a Mapped Diagnostics Context property that renders the value of `Environment.TickCount` at the time that the context item is rendered.

```
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

```
MappedDiagnosticsContext.Set("TickCount", MdcTickProperty.Default);
```

In the logging configuration, include:

```
${mdc:item=TickCount}
```

##Notes
When rendering context items, the item is passed to `String.Format` along with the current configuration's `DefaultCultureInfo` value.