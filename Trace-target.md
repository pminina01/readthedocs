Sends log messages through System.Diagnostics.Trace. 

Supported in .NET and Mono. 
##Configuration Syntax
```
<targets>
  <target xsi:type="Trace" name="String" layout="Layout" />
</targets>
```
##Parameters
###General Options
_name_ - Name of the target.
###Layout Options
_layout_ - Layout used to format log messages. Layout Required. Default: ${longdate}|${level:uppercase=true}|${logger}|${message}