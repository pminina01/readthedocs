Nested Diagnostics Context - a thread-local structure that keeps a stack
of strings and provides methods to output them in layouts.

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${ndc:bottomFrames=Integer:topFrames=Integer:separator=String}
```

##Parameters
###Rendering Options
* **bottomFrames** - Number of bottom stack frames to be rendered.Integer
* **topFrames** - Number of top stack frames to be rendered.Integer
* **separator** - Separator to be used for concatenating nested diagnostics context output