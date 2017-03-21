Thread identity information (name and authentication information). 

Supported in .NET and Mono.

## Configuration Syntax
```
${identity:authType=Boolean:separator=String:name=Boolean
          :isAuthenticated=Boolean}
```

## Parameters
### Rendering Options
* **authType** - Indicates whether to render Thread.CurrentPrincipal.Identity.AuthenticationType.Boolean Default: True
* **separator** - Separator to be used when concatenating parts of identity information. Default: :
* **name** - Indicates whether to render Thread.CurrentPrincipal.Identity.Name.Boolean Default: True
* **isAuthenticated** - Indicates whether to render Thread.CurrentPrincipal.Identity.IsAuthenticated.Boolean Default: True