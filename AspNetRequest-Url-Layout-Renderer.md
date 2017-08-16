Introduced in NLog.Web 4.3

ASP.NET Request URL.

Supported in .NET, .NET Core and Mono

## Configuration Syntax
```
${aspnet-request-url:IncludeHost=boolean:IncludePort=boolean:IncludeQueryString=boolean}
```

## Parameters
* **IncludeHost** - include the host name? Default is `true`.
* **IncludePort** - include the port number? Default is `false`.
* **IncludeQueryString** - include the querystring. Default is `false`.

## Examples

```
${aspnet-request-url:IncludeQueryString=true} - produces http://www.exmaple.com/?t=1
${aspnet-request-url:IncludeQueryString=false} - produces http://www.exmaple.com/
${aspnet-request-url:IncludePort=true} - produces http://www.exmaple.com:80/
${aspnet-request-url:IncludePort=false} - produces http://www.exmaple.com/
${aspnet-request-url:IncludePort=true:IncludeQueryString=true} - produces http://www.exmaple.com:80/?t=1    
```

Introduced in NLog.Web.AspNetCore 4.4.1 & NLog.Web 4.5.1. 

ASP.NET Request URL.

Supported in .NET, .NET Core and Mono

## Configuration Syntax
```
${aspnet-request-url:IncludeHost=boolean:IncludePort=boolean:IncludeQueryString=boolean:IncludeScheme=boolean}
```

## Parameters
* **IncludeScheme** - include the scheme. Default is `true`.

## Examples

```
${aspnet-request-url:IncludeScheme=true} - produces http://www.exmaple.com
${aspnet-request-url:IncludeScheme=false} - produces www.exmaple.com
 
```
