Escapes output of another layout using JSON rules. 

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${json-encode:jsonEncode=Boolean:inner=Layout}
```

or by using ambient property to modify output of other layout renderer:

```
${other:jsonEncode=Boolean}
```

##Parameters
###Transformation Options
* _jsonEncode_ - Indicates whether to apply JSON encoding. Boolean Default: True
* _inner_ - Wrapped layout. Layout


## Example

```

${event-properties:item=MyValue:jsonEncode=true}
```