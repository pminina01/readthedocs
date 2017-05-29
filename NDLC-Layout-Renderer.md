Nested Diagnostics Logical Context - Is the async version of [[NDC Layout Renderer|NDC-Layout-Renderer]]. It makes the nested context available to every logger executing on the current logical context. (Similar to "Thread Context" in Log4j)

Introduced in NLog 4.4.10

Supported in .NET 4.0 and 4.5.

## Configuration Syntax
```
${ndlc:bottomFrames=Integer:topFrames=Integer:separator=String}
```

## Parameters
### Rendering Options
* **bottomFrames** - Number of bottom stack frames to be rendered. `-1` is no limit. `Integer`. Default `-1`.
* **topFrames** - Number of top stack frames to be rendered. `-1` is no limit. `Integer`.  Default `-1`
* **separator** - Separator to be used for concatenating nested diagnostics context output. `string`. Default ` ` (space)

## Examples

```c#
using (NLog.NestedDiagnosticsLogicalContext.Push("Outer Scope"))
{
   Logger.Info("Hello Outer");
   await InnerOperationAsync();
}

static async Task InnerOperationAsync()
{
    using (NLog.NestedDiagnosticsLogicalContext.Push("Inner Scope"))
    {
        Logger.Info("Hello Inner");
        await Task.Yield();
    }
}
```