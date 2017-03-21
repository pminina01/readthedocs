Filters log entries based on a condition. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```xml
<targets>
  <target xsi:type="FilteringWrapper" name="String" condition="Condition">
    <target xsi:type="wrappedTargetType" ...target properties... />
  </target>
</targets>
```

## Parameters
### General Options
* **name** - Name of the target.

### Filtering Options
* **condition** - Condition expression. Log events who meet this condition will be forwarded to the wrapped target. Condition Required.