Writes log messages to the ASP.NET trace.

Supported in .NET and Mono

##Configuration Syntax
```
<targets>
  <target xsi:type="AspNetTrace" name="String" layout="Layout" />
</targets>
```

Read more about using the [Configuration File](Configuration file).

##Parameters
###General Options
name - Name of the target
###Layout Options
layout - Layout used to format log messages. [Layout](Layout) Required. Default: ${longdate}|${level:uppercase=true}|${logger}|${message}
###Remarks
Log entries can then be viewed by navigating to http://server/path/Trace.axd.

##Examples
In order to use this target, put the following code in the [configuration file](Configuration file) such as Web.nlog or NLog.config:
```
<?xml version="1.0" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <targets>
        <target name="aspnet" xsi:type="ASPNetTrace" layout="${logger} ${message}" />
    </targets>
    <rules>
        <logger name="*" minlevel="Debug" writeTo="aspnet" />
    </rules>
</nlog>
```

You can also configure the target programmatically, by putting the code in Application_Start event handler or similar:
```csharp
using System;
using System.Web;
 
using NLog;
using NLog.Targets;
 
namespace SomeWebApplication
{
    public class Global : System.Web.HttpApplication
    {
        //
        // this event handler is executed at the very start of the web application
        // so this is a good place to configure targets programmatically
        // 
        // alternative you could place this code in a static type constructor
        //
        protected void Application_Start(Object sender, EventArgs e)
        {
            ASPNetTraceTarget target = new ASPNetTraceTarget();
            target.Layout = "${logger} ${message}";
 
            NLog.Config.SimpleConfigurator.ConfigureForTargetLogging(target, LogLevel.Debug);
        }
    }
}
```