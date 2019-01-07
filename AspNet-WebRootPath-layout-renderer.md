ASP.NET WebRootPath 

Supported in [Asp.NET](https://docs.microsoft.com/dotnet/api/system.web.httpserverutility.mappath) and [Asp.NetCore](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.webrootpath)

> Introduced with NLog.Web.AspNetCore v4.5.0 and NLog.Web v4.5.2

## Configuration Syntax
```
${aspnet-webrootpath}
```

## Remarks
The web root (wwwroot) is the root directory from which static content is served, while the content root is the application base path.