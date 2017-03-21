Global Diagnostics Context - a dictionary structure to hold per-application-instance values.

Use the Global Diagnostics Context when you want to make certain information available to every logger in the current process.

The global context is one of the context. 

- When you need the context for all threads, use the [GDC](Gdc-Layout-Renderer). 
- When you need the context for one threads, use the [MDC](MDC-Layout-Renderer). 
- When you work with async, use the [MDLC](MDLC-Layout-Renderer)
- If the context is different for every message, use the [[Log event properties]]

As of NLog 4.1, the Global Diagnostics Context supports any `Object` type, not just `String`.

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${gdc:item=String}
```

## Parameters
### Rendering Options
* **item** - Name of the item. Required.

## Example
### Simple Properties
The following example demonstrates the basic usage of the Global Diagnostics Context.

```c#
GlobalDiagnosticsContext.Set("myDataBase","someValue");
GlobalDiagnosticsContext.Set("informationGroup", new { One = 1, Two = 2 });
GlobalDiagnosticsContext.Set("anyObject", anyObjectReferenceOrString);
```

Add the following to your logger configuration to reference the above properties:
```
${gdc:item=myDatabase}
${gdc:item=informationGroup}
${gdc:item=anyObject}
```

### Dynamic Properties
In some instances you may have thread-local information that you want to make available to all logger instances in the current process. This can be achieved with the [Mapped Diagnostics Context](https://github.com/NLog/NLog/wiki/MDC-Layout-Renderer), but requires that your create the property within the context of every thread that may reference it. Using Dynamic Properties and the Global Diagnostics Context, you can achieve the same result while only creating the property once.

```
public class ManagedThreadIdProperty
{
   public static readonly ManagedThreadIdProperty Default = new ManagedThreadIdProperty();

   private ManagedThreadIdProperty () 
   {
   }

   public override string ToString ()
   {
      return System.Threading.Thread.CurrentThread.ManagedThreadId.ToString();
   }
}
```

During initialization, add the following code:
```
GlobalDiagnosticsContext.Set("ManagedThreadId", ManagedThreadIdProperty.Default);
```

To reference the ManagedThreadId Global Diagnostics Context property.
```
${gdc:item=ManagedThreadId}
```

## Notes
When rendering context items, the item is passed to `String.Format` along with the current configuration's `DefaultCultureInfo` value.