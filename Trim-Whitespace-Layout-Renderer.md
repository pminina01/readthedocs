Trims the whitespace from the result of another layout renderer. 

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${trim-whitespace:trimWhiteSpace=Boolean:inner=Layout}
```

or by using ambient property to modify output of other layout renderer:

```
${other:trimWhiteSpace=Boolean}
```

##Parameters
###Transformation Options
* _trimWhiteSpace_ - Indicates whether lower case conversion should be applied. Boolean Default: True
* _inner_ - Wrapped layout. Layout