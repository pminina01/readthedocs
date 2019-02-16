Decodes text "encrypted" with ROT-13. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${rot13:inner=Layout:text=Layout}
```

## Parameters
### Transformation Options
* **inner** - Wrapped layout. Layout  

  > This parameter is not supported in:
  > * NLog v1.0 for .NET Compact Framework 1.0
  > * NLog v1.0 for .NET Compact Framework 2.0
  > * NLog v1.0 for .NET Framework 1.0
  > * NLog v1.0 for .NET Framework 1.1
  > * NLog v1.0 for .NET Framework 2.0

* **text** - Layout to be wrapped. Layout  
This variable is for backwards compatibility

## Remarks
See http://en.wikipedia.org/wiki/ROT13.