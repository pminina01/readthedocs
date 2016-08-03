Renders the assembly version of the entry assembly.


##Configuration Syntax
```
${assembly-version}
```


## Notes
- is uses [`Version.ToString`](https://msdn.microsoft.com/en-us/library/e31ax1a7(v=vs.110).aspx)
- Does not work in ASP.NET apps. Returns "Could not find entry assembly" in this case.