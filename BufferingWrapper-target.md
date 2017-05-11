A target that buffers log events and sends them in batches to the wrapped target. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```xml
<targets>
  <target xsi:type="BufferingWrapper"
          name="String"
          slidingTimeout="Boolean"
          bufferSize="Integer"
          flushTimeout="Integer">
    <target xsi:type="wrappedTargetType" ...target properties... />
  </target>
</targets>
```
## Parameters
### General Options
* **name** - Name of the target.
### Buffering Options
* **bufferSize** - Number of log events to be buffered. When the limit is reached, then a synchronously flush is performed. `Integer` Default: `100`

* **flushTimeout** - Timeout (in milliseconds) after a write, until the entire buffer is asynchronously flushed. Use `-1` to disable timed flushes. `Integer` Default: `-1`

* **slidingTimeout** - Indicates whether to use sliding _flushTimeout_. `Boolean` Default: `True`  
This value determines how the inactivity period is determined. If sliding timeout is enabled, the inactivity timer is reset after each write, if it is disabled - inactivity timer will count from the first event written to the buffer.

## Remarks

### Buffer and asynchronously writing

If `flushTimeout` is larger than `0`, then the messages are written asynchronously. There is then no need to use this target in combination with the `async` attribute or the [AsyncWrapper](https://github.com/NLog/NLog/wiki/AsyncWrapper-target).

When messages are written asynchronously, this is done in another thread. This means context information like thread-user-identity is different.

If the buffer is filled before the 'flushTimeout' fires and triggers the asynchronously flush, then the logging thread will be performing the flush, and be blocked by the operation.