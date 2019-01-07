Introduced in NLog Web.AspNetCore 4.4.0 & NLog.Web 4.5.0

Render Client IP address 

Supported in ASP.NET &  ASP.NET Core.

## Configuration Syntax
```
${aspnet-request-ip}
```

## Parameters

- _*CheckForwardedForHeader*_ - Should check value of X-Forwarded-For header (Default = false)
  > Introduced with NLog Web.AspNetCore 4.7.1 & NLog.Web 4.7.1

## Remarks

- AspNetCore - Uses underlying connection for this request. See [HttpContext.Connection.RemoteIpAddress](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.httpcontext.connection)
- AspNet - Returns the `REMOTE_ADDR`-ServerVariables