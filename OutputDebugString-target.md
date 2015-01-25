Outputs log messages through the OutputDebugString() Win32 API. 

Supported in .NET, Compact Framework and Mono.
##Configuration Syntax
```xml
<targets>
  <target xsi:type="OutputDebugString" name="String" layout="Layout" />
</targets>
```
Read more about using the [Configuration File](Configuration-file).
##Parameters
###General Options
_name_ - Name of the target.
###Layout Options
_layout_ - Layout used to format log messages. Required. Default: ${longdate}|${level:uppercase=true}|${logger}|${message}