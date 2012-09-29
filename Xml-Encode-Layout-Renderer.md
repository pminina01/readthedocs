Converts the result of another layout output to be XML-compliant. 

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${xml-encode:xmlEncode=Boolean:inner=Layout}
```

or by using ambient property to modify output of other layout renderer:

```
${other:xmlEncode=Boolean}
```

##Parameters
###Transformation Options
* _xmlEncode_ - Indicates whether to apply XML encoding. Boolean Default: True
* _inner_ - Wrapped layout. Layout