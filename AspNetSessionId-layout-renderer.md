ASP.NET Session ID. 

Supported in .NET and Mono

## Configuration Syntax
```
${aspnet-sessionid}
```

### Enable sessions in ASP.NET Core
Add line to `ConfigureServices()` in `Startup.cs`

```c#
public void ConfigureServices(IServiceCollection services)
{
     ...
     services.AddSession();
     ...
}
```

Add line to `Configure()` in `Startup.cs`

```c#
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
     ...
     app.UseSession();
     ...
}
```

See also [Configure session state](https://docs.microsoft.com/aspnet/core/fundamentals/app-state#configure-session-state)