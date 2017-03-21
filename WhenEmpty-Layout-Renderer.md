Outputs alternative layout when the inner layout produces empty result. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${whenEmpty:whenEmpty=Layout:inner=Layout}
```

or by using ambient property to modify output of other layout renderer:

```
${other:whenEmpty=Layout}
```

## Parameters
### Transformation Options
* **whenEmpty* - Layout to be rendered when original layout produced empty result. Layout Required.
* **inner** - Wrapped layout. Layout