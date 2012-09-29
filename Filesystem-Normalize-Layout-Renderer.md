Filters characters not allowed in the file names by replacing them with safe character. 

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${filesystem-normalize:fSNormalize=Boolean:inner=Layout}
```

or by using ambient property to modify output of other layout renderer:

```
${other:fSNormalize=Boolean}
```

##Parameters
###Advanced Options
* _fSNormalize_ - Indicates whether to modify the output of this renderer so it can be used as a part of file path (illegal characters are replaced with '_'). Boolean Default: True

###Transformation Options
* _inner_ - Wrapped layout. Layout