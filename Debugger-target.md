Writes log messages to the attached managed debugger. 

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
###Layout Options
* **footer** - Footer. [Layout](Data types)  
* **layout** - Text to be rendered. [Layout](Data types) Required. Default: `${longdate}|${level:uppercase=true}|${logger}|${message}`
* **header** - Header. [Layout](Data types)

### Examples
From [stackoverflow](http://stackoverflow.com/questions/252464/how-can-i-output-nlog-stuff-to-the-vs2008-output-window/260576#260576) 
```
 <targets>
        <target name="debugger" xsi:type="Debugger" layout="${logger}::${message}"/>
  </targets>

  <rules>
    <logger name="*" minlevel="Trace" writeTo="debugger" />
  </rules>
```