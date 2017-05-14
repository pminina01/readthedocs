Renders the assembly version of the entry or a named assembly.

## Configuration Syntax
```
${assembly-version:name=string}
```
## Parameters

* **name** - The name of the assembly. Note will load it. If `null`, will find the entry assembly. Introduced in NLog 4.3.7

## Examples

```
${assembly-version:NLogAutloadExtension}
```

## Notes
- is uses [`Version.ToString`](https://msdn.microsoft.com/en-us/library/e31ax1a7(v=vs.110).aspx)
- For ASP.NET / ASP.NET Core you need NLog.Web 4.5.0 /  NLog Web.AspNetCore 4.4.0 