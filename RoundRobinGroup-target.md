Distributes log events to targets in a round-robin fashion. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```xml
<targets>
  <target xsi:type="RoundRobinGroup" name="String">
    <target xsi:type="wrappedTargetType" ... />
    <target xsi:type="wrappedTargetType" ... />
    ...
    <target xsi:type="wrappedTargetType" ... />
  </target>
</targets>
```

## Parameters
### General Options
* **name** - Name of the target.

### Performance Options
* **OptimizeBufferReuse** - Reduce logging overhead, by allowing buffer reuse. Default: `True`
  > Introduced with NLog v4.4.2. Default became `True` until NLog v4.5