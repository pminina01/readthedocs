Converts the result of another layout output to upper case. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${uppercase:uppercase=Boolean:inner=Layout:culture=Culture}
```

or by using ambient property to modify output of other layout renderer:

```
${other:uppercase=Boolean}
```

## Parameters
### Transformation Options
* **inner** - Wrapped layout. Layout.  Default attribute.
* **uppercase** - Indicates whether upper case conversion should be applied. Default `true` with Inner, required when using as ambient.
* **culture** - Culture used for rendering. Culture

## Examples

```
${uppercase:${level}}
${uppercase:Inner=${level}}
${level:uppercase=true}  //NB: `${level:uppercase}` isn't correct, 
                         // as the parser will read `uppercase` as a default parameter of `Level` 


```