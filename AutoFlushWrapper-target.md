Causes a flush on a wrapped target if LogEvent satisfies provided condition.  
If condition isn't set, a flush will occur after each write.

Supported in .NET, Silverlight, Compact Framework and Mono.
## Configuration Syntax
```xml
<targets>
  <target xsi:type="AutoFlushWrapper" name="String" condition="Condition">
    <target xsi:type="wrappedTargetType" ...target properties... />
  </target>
</targets>
```

## Parameters
### General Options
* **name** - Name of the target.  
* **condition** - [Condition](https://github.com/NLog/NLog/wiki/When-Filter#conditions) is expression used to determine if flush must be executed. (*introduced in NLog 4.4*)
* **asyncFlush** - Delay the flush until the LogEvent has been confirmed as written. Default `true`. (*introduced in NLog 4.4.6*)

## Examples
Flush into target on each write
```xml
<?xml version="1.0" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <targets>
        <target name="file" xsi:type="AutoFlushWrapper">
            <target xsi:type="File" fileName="${basedir}/file.txt" />
        </target>
    </targets>
    <rules>
        <logger name="*" minlevel="Debug" writeTo="file" />
    </rules>
</nlog>
```


Flush into target, if LogEvent level >= Warn (*introduced in NLog 4.4*)
```xml
<?xml version="1.0" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <targets>
        <target name="file" xsi:type="AutoFlushWrapper" condition="level >= LogLevel.Warn">
            <target xsi:type="File" fileName="${basedir}/file.txt" />
        </target>
    </targets>
    <rules>
        <logger name="*" minlevel="Debug" writeTo="file" />
    </rules>
</nlog>
```