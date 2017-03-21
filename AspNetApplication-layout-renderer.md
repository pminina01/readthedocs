ASP.NET Application variable. 

Supported in .NET and Mono. 

Not supported in ASP.NET Core - [ServerVariables are non-existing in ASP.NET Core. ](http://stackoverflow.com/questions/25849217/vnext-server-variables-missing)

## Configuration Syntax
```
${aspnet-application:variable=String}
```

## Parameters
### Rendering Options
* **variable** - Variable name. Required.

## Remarks
Use this layout renderer to insert the value of the specified variable stored in the ASP.NET Application dictionary