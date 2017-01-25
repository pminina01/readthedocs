Writes log messages to the attached managed debugger. 

Supported in .NET, Silverlight and Mono
##Configuration Syntax
```xml
<targets>
  <target xsi:type="Debugger"
          name="String"
          footer="Layout"
          layout="Layout"
          header="Layout" />
</targets>
```
Read more about using the [Configuration File](Configuration file).
##Parameters
###General Options
_name_ - Name of the target.
###Layout Options
_footer_ - Footer. [Layout](Data types)  
_layout_ - Text to be rendered. [Layout](Data types) Required. Default: ${longdate}|${level:uppercase=true}|${logger}|${message}  
_header_ - Header. [Layout](Data types)

###Examples
From [stackoverflow](http://stackoverflow.com/questions/252464/how-can-i-output-nlog-stuff-to-the-vs2008-output-window/260576#260576) 
```
 <targets>
        <target name="debugger" xsi:type="Debugger" layout="${logger}::${message}"/>
  </targets>

  <rules>
    <logger name="*" minlevel="Trace" writeTo="debugger" />
  </rules>
```