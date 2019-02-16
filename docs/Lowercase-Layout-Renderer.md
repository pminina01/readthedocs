Converts the result of another layout output to lower case. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${lowercase:lowercase=Boolean:inner=Layout:culture=Culture}
```

or by using ambient property to modify output of other layout renderer:

```
${other:lowercase=Boolean}
```

## Parameters
### Transformation Options
* **lowercase** - Indicates whether lower case conversion should be applied. Boolean Default: True. Required when using as ambient. 
* **inner** - Wrapped layout. Layout
* **culture** - Culture used for rendering. Culture

## Note
`${level:lowercase}` isn't correct, as the parser will read `lowercase` as a default parameter of `Level` 