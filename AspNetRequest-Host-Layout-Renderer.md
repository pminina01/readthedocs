Introduced in NLog.Web 4.3

ASP.NET Host Renderer. 

Supported in [ASP.NET Core](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.httprequest.host) and [ASP.NET](https://docs.microsoft.com/en-us/dotnet/api/system.web.httprequest.userhostname?view=netframework-4.7.2)

## Configuration Syntax
```
${aspnet-request-host}
```

## Remarks
- ASP.NET Core returns the `Host`-Header
- ASP.NET returns the `REMOTE_ADDR`-ServerVariable

See also [[AspNet Request IP Layout Renderer]]