Writes log messages to the attached managed debugger. See also [System.Diagnostics.Debugger.Log](https://msdn.microsoft.com/en-us/library/system.diagnostics.debugger.log.aspx)

Supported in .NET, Silverlight and Mono

## Configuration Syntax
```xml
<targets>
  <target xsi:type="Debugger"
          name="String"
          footer="Layout"
          layout="Layout"
          header="Layout" />
</targets>
```
Read more about using the [[Configuration File]].

## Parameters
### General Options
* **name** - Name of the target.

### Layout Options
* **footer** - Footer. [Layout](Data-types)  
* **layout** - Text to be rendered. [Layout](Data-types) Required. Default: `${longdate}|${level:uppercase=true}|${logger}|${message}`
* **header** - Header. [Layout](Data-types)

### Performance Options
* **OptimizeBufferReuse** - Reduce logging overhead, by allowing buffer reuse. Default: `True`
  > Introduced with NLog v4.4.2. Default became `True` with NLog v4.5

### Examples
From [stackoverflow](https://stackoverflow.com/a/260576/767425) 
```xml
<targets>
  <target name="debugger" xsi:type="Debugger" layout="${logger}::${message}"/>
</targets>

<rules>
  <logger name="*" minlevel="Trace" writeTo="debugger" />
</rules>
```