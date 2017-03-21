Sends log messages through System.Diagnostics.Trace. 

Supported in .NET and Mono.

## Configuration Syntax
```xml
<targets>
  <target xsi:type="Trace" name="String" layout="Layout" />
</targets>
```

## Parameters
### General Options
* **name** - Name of the target.
###Layout Options
* **layout** - Layout used to format log messages. Layout Required. Default: `${longdate}|${level:uppercase=true}|${logger}|${message}`