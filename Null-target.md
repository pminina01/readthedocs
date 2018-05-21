Discards log messages. Used mainly for debugging and benchmarking. 

Supported in .NET, Silverligt, Compact Framework and Mono.

## Configuration Syntax
```xml
<targets>
  <target xsi:type="Null" name="String" formatMessage="Boolean" layout="Layout" />
</targets>
```
Read more about using the [[Configuration File]].

## Parameters
### General Options
* **name** - Name of the target.

### Layout Options
* **formatMessage** - Indicates whether to perform layout calculation. [Boolean](Data-types) Default: False

* **layout** - Layout used to format log messages. [Boolean](Data-types) Required. Default: `${longdate}|${level:uppercase=true}|${logger}|${message}`

### Performance Options
* **OptimizeBufferReuse** - Reduce logging overhead, by allowing buffer reuse. Default: `True`
  > Introduced with NLog v4.4.2. Default became `True` with NLog v4.5


## Example

```xml
<targets>
  <target xsi:type="Null" name="BlackHole" formatMessage="false"  />
</targets>
<rules>
   <!-- ignore events written that are written to a logger which starts with "Namespace." -->
   <logger name="Namespace.*" minlevel="Debug" writeTo="BlackHole" final="true" />     
</rules>
```