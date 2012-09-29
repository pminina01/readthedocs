Applies padding to another layout output. 

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${pad:padCharacter=Char:padding=Integer:fixedLength=Boolean
     :inner=Layout}
```

or by using ambient property to modify output of other layout renderer:

```
${other:padCharacter=Char}
```

##Parameters
###Transformation Options
* _padCharacter_ - Padding character. Char Default:
* _padding_ - Number of characters to pad the output to. Integer  
Positive padding values cause left padding, negative values cause right padding to the desired width.
* _fixedLength_ - Indicates whether to trim the rendered text to the absolute value of the padding length. Boolean Default: False
* _inner_ - Wrapped layout. Layout