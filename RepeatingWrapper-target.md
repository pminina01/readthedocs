Repeats each log event the specified number of times. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
<targets>
  <target xsi:type="RepeatingWrapper" name="String" repeatCount="Integer">
    <target xsi:type="wrappedTargetType" ...target properties... />
  </target>
</targets>
```
## Parameters
### General Options
* **name** - Name of the target.
### Repeating Options
* **repeatCount** - Number of times to repeat each log message. Integer Default: 3