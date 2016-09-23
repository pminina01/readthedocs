Logs text to Windows.Forms.Control.Text property control of specified Name. 

Supported in .NET
##Configuration Syntax
```xml
<targets>
  <target xsi:type="FormControl"
          name="String"
          layout="Layout"
          append="Boolean"
          reverseOrder="Boolean"
          controlName="String"
          formName="String" />
</targets>
```
Read more about using the [Configuration File](Configuration-file).
##Parameters
###General Options
_name_ - Name of the target.
###Layout Options
_layout_ - Layout used to format log messages. [Layout](Data-types) Required. Default: ${longdate}|${level:uppercase=true}|${logger}|${message}
###Form Options
_append_ - Indicates whether log text should be appended to the text of the control instead of overwriting it. [Boolean](Data-types) Default: True

_reverseOrder_ - Indicates whether log text should be appended or prepended. [Boolean](Data-types) Default: False

_controlName_ - Name of control to which NLog will log write log text. Required.

_formName_ - Name of the Form on which the control is located.