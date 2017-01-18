ASP.NET Request variable. 

Supported in .NET and Mono


##Legacy
This layout renderer is broken down to separate layout renders who are more ASP.NET Core compatible / future proof:


* [${aspnet-Request-Cookie}](https://github.com/NLog/NLog/wiki/AspNetRequest-Cookie-Layout-Renderer) - ASP.NET Request cookie content. 
* [${aspnet-Request-Host}](https://github.com/NLog/NLog/wiki/AspNetRequest-Host-Layout-Renderer) - ASP.NET Request host.
* [${aspnet-Request-Method}](https://github.com/NLog/NLog/wiki/AspNetRequest-Method-Layout-Renderer) - ASP.NET Request method (GET, POST etc).
* [${aspnet-Request-QueryString}](https://github.com/NLog/NLog/wiki/AspNetRequest-QueryString-Layout-Renderer) - ASP.NET Request querystring.
* [${aspnet-Request-Referrer}](https://github.com/NLog/NLog/wiki/AspNetRequest-Referrer-Renderer) - ASP.NET Request referrer.
* [${aspnet-Request-UserAgent}](https://github.com/NLog/NLog/wiki/AspNetRequest-UserAgent-Layout-Renderer) - ASP.NET Request useragent.
* [${aspnet-Request-Url}](https://github.com/NLog/NLog/wiki/AspNetRequest-Url-Layout-Renderer) - ASP.NET Request URL.

##Configuration Syntax
```
${aspnet-request:cookie=String:serverVariable=String:queryString=String
                :item=String:form=String:header=String}
```

##Parameters
###Rendering Options
* **cookie** - Cookie to be rendered.
* **header** - Request header. Introduced in NLog.Web 4.2
* **serverVariable** - ServerVariables item to be rendered. See for possible options: [msdn](https://msdn.microsoft.com/en-us/library/ms524602(v=vs.90).aspx). Not supported in ASP.NET Core. 
* **queryString** - QueryString variable to be rendered.
* **item** - Item name. The QueryString, Form, Cookies, or ServerVariables collection variables having the specified name are rendered.
* **form** - Form variable to be rendered.

##Remarks
Use this layout renderer to insert the value of the specified parameter of the ASP.NET Request object. This renderer requires the NLog.Web package.

##Examples
Full URL without domain, eg "default.aspx?id=512"

` ${aspnet-request:serverVariable=HTTP_URL}${aspnet-request:queryString}` 