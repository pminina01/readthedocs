Calls the specified static method on each log message and passes contextual parameters to it. 

Supported in .NET, Silverlight, Compact Framework and Mono.
##Configuration Syntax
```xml
<targets>
  <target xsi:type="MethodCall"
          name="String"
          methodName="String"
          className="String">
    <parameter layout="Layout" name="String" type="System.Type"/><!-- repeated -->
  </target>
</targets>
```
Read more about using the [Configuration File](Configuration-file).
##Parameters
###General Options
_name_ - Name of the target.
###Invocation Options
_methodName_ - Method name. The method must be public and static.

_className_ - Class name.
###Parameter Options
_parameters_ - The array of parameters to be passed. [Collection](Data-types)  
Each collection item is represented by \<parameter /> element with the following attributes:
  * _layout_ - Layout that should be use to calcuate the value for the parameter. [Layout](Data-types) Required.
  * _name_ - Name of the parameter.
  * _type_ - Type of the parameter. [System.Type](Data-types)

##Examples
###Logging to a static method
In order to send all logs to a static method, use the following configuration file:
```xml
<?xml version="1.0" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <targets>
        <target name="m" xsi:type="MethodCall" className="SomeNamespace.MyClass, MyAssembly" methodName="LogMethod">
            <parameter layout="${level}" />
            <parameter layout="${message}" />
        </target>
    </targets>
 
    <rules>
        <logger name="*" minlevel="Debug" writeTo="m" />
    </rules>
</nlog>
```

Per the configuration, the log method needs to be called "LogMethod" be declared in "SomeNamespace.MyClass" class. The class must be compiled to MyAssembly.dll. Each parameter of the log method must correspond to \<parameter /> entry in the target configuration.

```csharp
namespace SomeNamespace
{
    using System;
 
    public class MyClass
    {
        public static void LogMethod(string level, string message)
        {
            Console.WriteLine("l: {0} m: {1}", level, message);
        }
    }
}
```

Names of parameters are not important, only their order is. The default type of each parameter is string, but it can be overridden by adding type attribute to <parameter /> element.

It is also possible to configure logging using [Configuration API](Configuration-API):

```csharp
using System;
 
using NLog;
using NLog.Targets;
using System.Diagnostics;
 
public class Example
{
    public static void LogMethod(string level, string message)
    {
        Console.WriteLine("l: {0} m: {1}", level, message);
    }
 
    static void Main(string[] args)
    {
        MethodCallTarget target = new MethodCallTarget();
        target.ClassName = typeof(Example).AssemblyQualifiedName;
        target.MethodName = "LogMethod";
        target.Parameters.Add(new MethodCallParameter("${level}"));
        target.Parameters.Add(new MethodCallParameter("${message}"));
 
        NLog.Config.SimpleConfigurator.ConfigureForTargetLogging(target, LogLevel.Debug);
 
        Logger logger = LogManager.GetLogger("Example");
        logger.Debug("log message");
        logger.Error("error message");
    }
}
```