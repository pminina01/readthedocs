Mapped Diagnostics Context - a thread-local structure that keeps a dictionary
of strings and provides methods to output them in layouts. 
 
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
The following example demonstrates a Mapped Diagnostics Context property that renders the value of `Environment.TickCount` at the time that it is rendered.

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

```
MappedDiagnosticsContext.Set("TickCount", MdcTickProperty.Default);
```
##Notes
When rendering context items, the item is passed to `String.Format` along with the current configuration's `DefaultCultureInfo` value.