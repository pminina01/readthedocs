Writes log messages to the console. 

Supported in .NET, Silverlight, Compact Framework and Mono
##Configuration Syntax
```
<targets>
  <target xsi:type="Console"
          name="String"
          layout="Layout"
          footer="Layout"
          header="Layout"
          error="Boolean" />
</targets>
```
Read more about using the [Configuration File](Configuration file).
##Parameters
###General Options
_name_ - Name of the target.
###Layout Options
_layout_ - Text to be rendered. [Layout](Layout) Required. Default: ${longdate}|${level:uppercase=true}|${logger}|${message}  
_footer_ - Footer. [Layout](Layout)  
_header_ - Header. [Layout](Layout)
###Console Options
_error_ - Indicates whether to send the log messages to the standard error instead of the standard output. [Boolean](Data types) Default: False
> This parameter is not supported in:
> * NLog v1.0 for .NET Compact Framework 1.0
> * NLog v1.0 for .NET Compact Framework 2.0
> * NLog v2.0 for .NET Compact Framework 2.0
NLog v2.0 for .NET Compact Framework 3.5