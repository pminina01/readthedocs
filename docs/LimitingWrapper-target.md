Limiting Wrapper
===================
Limits the number of logs written to the wrapped target in a given time interval.

Supported in .NET, Silverlight, Compact Framework and Mono.

Introduced in NLog 4.4.

## Configuration Syntax
```xml
<targets>
  <target xsi:type="LimitingWrapper"
          name="String"
          messageLimit="Integer"
          interval="TimeSpan">
    <target xsi:type="wrappedTargetType" ...target properties... />
  </target>
</targets>
```
## Parameters

### General Options
* **name** - Name of the target.

### Limiting Options
* **messageLimit** - Indicates the maximum number of log events written per Interval. Log events in the current interval received after the message limit has been reached will be discarded. `Integer` Default: `1000`

* **interval** - Indicates a time interval in which messages will be written up to the maximum number of messages (_messageLimit_). `TimeSpan`Default: `"01:00"` (1 hour)

### Performance Options
* **OptimizeBufferReuse** - Reduce logging overhead, by allowing buffer reuse. Default: `True`
  > Introduced with NLog v4.4.2. Default became `True` with NLog v4.5