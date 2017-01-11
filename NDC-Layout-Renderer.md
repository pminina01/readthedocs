Nested Diagnostics Context - a thread-local structure that keeps a stack
of strings and provides methods to output them in layouts.

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${ndc:bottomFrames=Integer:topFrames=Integer:separator=String}
```

##Parameters
###Rendering Options
* **bottomFrames** - Number of bottom stack frames to be rendered. `-1` is no limit. `Integer`. Default `-1`.
* **topFrames** - Number of top stack frames to be rendered. `-1` is no limit. `Integer`.  Default `-1`
* **separator** - Separator to be used for concatenating nested diagnostics context output. `string`. Default ` ` (space)

## Examples

### One level

```c#
NestDiagnosticsContext.Push("entering method X");
... // log here
NestDiagnosticsContext.Pop(); //leaving methods
```

Then in the log config:

    ${ndc}

logs `entering method X`  if logged between `push()`  and `pop()`


### Multiple levels
 ```c#
NestDiagnosticsContext.Push("entering method X1");
NestDiagnosticsContext.Push("entering method X2");
... // log here
NestDiagnosticsContext.Pop(); //leaving method X2
NestDiagnosticsContext.Pop(); //leaving method X1
```

logs `entering method X1 entering method X2`