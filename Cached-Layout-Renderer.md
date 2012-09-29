Applies caching to another layout output. 

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${cached:cached=Boolean:inner=Layout}
```

or by using ambient property to modify output of other layout renderer:

```
${other:cached=Boolean}
```

##Parameters
###Caching Options
* _cached_ - Indicates whether this CachedLayoutRendererWrapper is enabled. Boolean Default: True
###Transformation Options
* _inner_ - Wrapped layout. Layout

##Remarks
The value of the inner layout will be rendered only once and reused subsequently.