ASP.NET EnvironmentName (`ASPNETCORE_ENVIRONMENT`)

Supported in [Asp.NetCore](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname)

> Introduced with NLog.Web.AspNetCore v4.4.0

## Configuration Syntax
```
${aspnet-environment}
```

## Remarks
The host automatically sets this property to the value of the "ASPNETCORE_ENVIRONMENT" environment variable, or "environment" as specified in any other configuration source.