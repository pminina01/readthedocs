ASP.NET Session variable. 

Supported in .NET and Mono

## Configuration Syntax
```
${aspnet-session:variable=String:evaluateAsNestedProperties:boolean}
```

## Parameters
### Rendering Options
* **variable** - Session variable name.
* **EvaluateAsNestedProperties** - boolean. Default: `false`. Evaluate the `variable` as nested properties. The dots in the `variable` are special interpreted. See example below.

## Remarks
Use this layout renderer to insert the value of the specified variable stored in the ASP.NET Session dictionary.

## Examples

Log the username in the session.

In the C# code:
```c#
Session["username"] = "johnDoe";
```

Config:
```xml
<?xml version="1.0" encoding="utf-8" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

    <targets>
        <target name="logfile" xsi:type="File" fileName="file.txt" />
    </targets>

    <rules>
        <logger name="*" minlevel="Info" writeTo="logfile" layout="${aspnet-session:Variable=Username}" />
    </rules>
</nlog>
```
Will print "JohnDoe"
#### EvaluateAsNestedProperties

In the C# code:
```c#
Session["user"] = new UserInfo { Name= "johnDoe", Id = 100};
```

Config:
```xml
<?xml version="1.0" encoding="utf-8" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

    <targets>
        <target name="logfile" xsi:type="File" fileName="file.txt" />
    </targets>

    <rules>
        <logger name="*" minlevel="Info" writeTo="logfile" layout="${aspnet-session:Variable=User.Name:EvaluateAsNestedProperties=true}" />
    </rules>
</nlog>
```
Will print "JohnDoe"
