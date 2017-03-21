ASP.NET Item variable.
Use this layout renderer to insert the value of the specified variable stored 
 in the ASP.NET `HttpContext.Current.Items` dictionary.

Supported in .NET and Mono

## Configuration Syntax
```
${aspnet-item:variable=String;evaluateAsNestedProperties:boolean}
```

## Parameters
### Rendering Options
* **variable** - Variable name.
* _EvaluateAsNestedProperties_ - boolean. Default: `false`. Evaluate the  as nested properties. The dots in the `variable` are special interpreted. See example below.


## Examples

<para>You can set the value of an ASP.NET Item variable by using the following code:</para>
	
Example usage of `${aspnet-item}`


```c#
HttpContext.Current.Items["myvariable"] = 123;
HttpContext.Current.Items["stringvariable"] = "aaa BBB";
HttpContext.Current.Items["anothervariable"] = DateTime.Now;

${aspnet-item:variable=myvariable} - produces "123"
${aspnet-item:variable=anothervariable} - produces "01/01/2006 00:00:00"
${aspnet-item:variable=anothervariable:culture=pl-PL} - produces "2006-01-01 00:00:00"
${aspnet-item:variable=myvariable:padding=5} - produces "  123"
${aspnet-item:variable=myvariable:padding=-5} - produces "123  "
${aspnet-item:variable=stringvariable:upperCase=true} - produces "AAA BBB"
```