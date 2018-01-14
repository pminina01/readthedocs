Sends log messages to a randomly selected target. 

Supported in .NET, Silverligt, Compact Framework and Mono.

## Configuration Syntax
```xml
<targets>
  <target xsi:type="RandomizeGroup" name="String">
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