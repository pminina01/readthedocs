Introduced in NLog.Web 4.3

ASP.NET Cookie Variable. 

Supported in ASP.NET, ASP.NET Core and Mono

## Configuration Syntax
```
${aspnet-request-cookie:CookieNames=Keys;OutputFormat:AspNetLayoutOutputFormat}
```

## Parameters
### Rendering Options
* **Keys** - Cookie name. A list of keys can be passed as a Comma separated value. Eg: Key1, Key2
* **OutputFormat** - AspNetLayoutOutputFormat. Possible Values: `FLAT`, `JSON`. Default: `flat`. Evaluate the `cookiename` and `values` flat string. See example below.

## Remarks
Use this layout renderer to insert the value of the specified cookie stored in the ASP.NET Request Cookies Collection.

## Examples

Log the username in the session.

In the C# code:
```c#
Request.Cookies["username"] = "johnDoe";
```

Config:
```xml
<?xml version="1.0" encoding="utf-8" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <extensions>
        <add assembly="NLog.Web" />
    </extensions>

    <targets>
        <target name="logfile" xsi:type="File" fileName="file.txt" />
    </targets>

    <rules>
        <logger name="*" minlevel="Info" writeTo="logfile" layout="${aspnet-request-cookie:CookieNames=username}" />
    </rules>
</nlog>
```
Will print 
```
"JohnDoe"
```

In the C# code:
```c#
Request.Cookies["username"] = "johnDoe";
```

Config:
```xml
<?xml version="1.0" encoding="utf-8" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <extensions>
        <add assembly="NLog.Web" />
    </extensions>

    <targets>
        <target name="logfile" xsi:type="File" fileName="file.txt" />
    </targets>

    <rules>
        <logger name="*" minlevel="Info" writeTo="logfile" layout="${aspnet-request-cookie:CookieNames=username;OutputFormat=JSON}" />
    </rules>
</nlog>
```
Will print 
```json
"{"username"="JohnDoe"}"
```
