The environment variable like Path, TMP, PROCESSOR_ARCHITECTURE etc.

Supported in .NET and Mono

## Configuration Syntax
```
${environment:variable=String}
```

## Parameters
### Rendering Options
* _variable_ - Name of the environment variable. Required. Examples: Path, TMP, USERPROFILE, PROCESSOR_ARCHITECTURE

## Remarks

- To list all environment variables in your system: `Environment.GetEnvironmentVariables()`

- These are the environment variables, not the properties listed at  [Environment Class on MSDN](https://msdn.microsoft.com/en-us/library/system.environment(v=vs.110).aspx)

## Example
log file for 32 bits systems in folder 32 and otherwise in folder 64

```xml
<target 
   xsi:type="File"
   name="file1" 
   fileName="c:\temp\${when:when='${environment:PROCESSOR_ARCHITECTURE}'='X86':inner=32:else=64}\file.log" />
```
