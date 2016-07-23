ASP.NET Request variable. 

Supported in .NET and Mono

##Configuration Syntax
```
${aspnet-request:cookie=String:serverVariable=String:queryString=String
                :item=String:form=String:header=String}
```

##Parameters
###Rendering Options
* **cookie** - Cookie to be rendered.
* **header** - Request header. Introduced in NLog.Web 4.2
* **serverVariable** - ServerVariables item to be rendered. See for possible options: [msdn](https://msdn.microsoft.com/en-us/library/ms524602(v=vs.90).aspx)
* **queryString** - QueryString variable to be rendered.
* **item** - Item name. The QueryString, Form, Cookies, or ServerVariables collection variables having the specified name are rendered.
* **form** - Form variable to be rendered.

##Remarks
Use this layout renderer to insert the value of the specified parameter of the ASP.NET Request object. This renderer requires the NLog.Exended.dll package.

##Examples
Full URL without domain, eg "default.aspx?id=512"

` ${aspnet-request:serverVariable=HTTP_URL}${aspnet-request:queryString}` 