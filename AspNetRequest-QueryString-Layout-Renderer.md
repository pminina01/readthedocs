Introduced in NLog.Web 4.3

ASP.NET Query String Variable. 

Supported in .NET, .NET Core and Mono

## Configuration Syntax
```
${aspnet-request-querystring:QueryStringKeys=Keys;OutputFormat:AspNetLayoutOutputFormat}
```

## Parameters
### Rendering Options
* **Keys** - Query String Key. A list of keys can be passed as a Comma separated value. Eg: Key1, Key2. Since NLog.Web 4.3.1 optional. No value is all query string values
* **OutputFormat** - AspNetLayoutOutputFormat. Possible Values: `FLAT`, `JSON`. Default: `flat`. Evaluate the `querysttring` and `values` flat string. See example below.

## Remarks
Use this layout renderer to insert the value of the specified cookie stored in the ASP.NET Query String Collection.

## Examples

Log the username in the session.

In the C# code:
```c#
Response.Redirect("myPage.aspx?id=1");
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
        <logger name="*" minlevel="Info" writeTo="logfile" layout="${aspnet-request-querystring:QueryStringKeys=id}" />
    </rules>
</nlog>
```
Will print 
```
Id:1
```

In the C# code:
```c#
Response.Redirect("myPage.aspx?id=1");
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
        <logger name="*" minlevel="Info" writeTo="logfile" layout="${aspnet-request-querystring:QueryStringKeys=id;OutputFormat=JSON}" />
    </rules>
</nlog>
```
Will print 
```json
[{"Id":"1"}]
```
