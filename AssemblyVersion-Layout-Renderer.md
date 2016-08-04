Renders the assembly version of the entry or a named assembly.


##Configuration Syntax
```
${assembly-version:name=string}
```
## Parameters

- _name_: the name of the assembly. Note will load it. If `null`, will find the entry assembly

## Examples

```
${assembly-version:NLogAutloadExtension}
```



## Notes
- is uses [`Version.ToString`](https://msdn.microsoft.com/en-us/library/e31ax1a7(v=vs.110).aspx)
- Does not work in ASP.NET apps. Returns "Could not find entry assembly" in this case.