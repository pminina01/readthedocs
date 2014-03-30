ASP.NET Request variable. 

Supported in .NET and Mono

##Configuration Syntax
```
${aspnet-request:cookie=String:serverVariable=String:queryString=String
                :item=String:form=String}
```

##Parameters
###Rendering Options
* **cookie** - Cookie to be rendered.
* **serverVariable** - ServerVariables item to be rendered.
* **queryString** - QueryString variable to be rendered.
* **item** - Item name. The QueryString, Form, Cookies, or ServerVariables collection variables having the specified name are rendered.
* **form** - Form variable to be rendered.

##Remarks
Use this layout renderer to insert the value of the specified parameter of the ASP.NET Request object. This renderer requires the NLog.Exended.dll package.