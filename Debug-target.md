Mock target - useful for testing. 

Supported in .NET, Silverlight, Compact Framework and Mono
##Configuration Syntax
```xml
<targets>
  <target xsi:type="Debug" name="String" layout="Layout" />
</targets>
```
Read more about using the [Configuration File](Configuration file).
##Parameters
###General Options
_name_ - Name of the target.
###Layout Options
_layout_ - Layout used to format log messages. [Layout](Data types) Required. Default: ${longdate}|${level:uppercase=true}|${logger}|${message}