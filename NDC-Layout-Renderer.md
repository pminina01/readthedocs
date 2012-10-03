Nested Diagnostic Context item. Provided for compatibility with log4net. 

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