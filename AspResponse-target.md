Outputs log messages through the ASP Response object. 

Supported in .NET and Mono

## Configuration Syntax
```xml
<targets>
  <target xsi:type="AspResponse" name="String" addComments="Boolean" layout="Layout" />
</targets>
```
Read more about using the [configuration file](Configuration file).

## Parameters

### General Options
* **name** - Name of the target

### Layout Options
* **addComments** - Indicates whether to add `<!-- -->` comments around all written texts. [Boolean](Data types)
* **layout** - Layout used to format log messages. [Layout](Layout) Required. Default:  `{longdate}|${level:uppercase=true}|${logger}|${message}`

## Examples
This target is usable when using classic ASP (not ASP.NET). In order to use this target, put the following code in the [configuration file](Configuration file) which is loaded into the web server process:
```xml
<?xml version="1.0" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <targets>
        <target name="aspnet" xsi:type="ASPResponse" layout="${logger} ${message}" />
    </targets>
    <rules>
        <logger name="*" minlevel="Debug" writeTo="aspnet" />
    </rules>
</nlog>
```