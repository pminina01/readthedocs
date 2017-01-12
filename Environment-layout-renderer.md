The environment variable. 

Supported in .NET and Mono

##Configuration Syntax
```
${environment:variable=String}
```

##Parameters
###Rendering Options
* **variable** - Name of the environment variable. Required. Examples: Path, TMP, USERPROFILE, PROCESSOR_ARCHITECTURE

Remarks

- To list all environment variables in your system: `Environment.GetEnvironmentVariables()`
`
- These are the environment variables, not the properties listed at  [Environment Class on MSDN](https://msdn.microsoft.com/en-us/library/system.environment(v=vs.110).aspx)