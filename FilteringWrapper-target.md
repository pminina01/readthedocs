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

### Performance Options
* **OptimizeBufferReuse** - Reduce logging overhead, by allowing buffer reuse. Default: `True`
  > Introduced with NLog v4.4.2. Default became `True` until NLog v4.5