Escapes output of another layout using JSON rules. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${json-encode:jsonEncode=Boolean:inner=Layout}
```

or by using ambient property to modify output of other layout renderer:

```
${other:jsonEncode=Boolean}
```

## Parameters
### Transformation Options
* **jsonEncode** - Indicates whether to apply JSON encoding. Boolean Default: True
* **escapeUnicode** - Indicates whether it should escape unicode characters using **\u**. Boolean Default: True
  * Introduced with NLog 4.4.7
* **inner** - Wrapped layout. Layout


## Example

```
${event-properties:item=MyValue:jsonEncode=true}
```