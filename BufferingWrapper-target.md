A target that buffers log events and sends them in batches to the wrapped target. 

Supported in .NET, Silverlight, Compact Framework and Mono.
##Configuration Syntax
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
##Parameters
###General Options
_name_ - Name of the target.
###Buffering Options
_slidingTimeout_ - Indicates whether to use sliding timeout. `Boolean` Default: `True`  
This value determines how the inactivity period is determined. If sliding timeout is enabled, the inactivity timer is reset after each write, if it is disabled - inactivity timer will count from the first event written to the buffer.

_bufferSize_ - Number of log events to be buffered. `Integer` Default: `100`

_flushTimeout_ - Timeout (in milliseconds) after which the contents of buffer will be flushed if there's no write in the specified period of time. Use `-1` to disable timed flushes. `Integer` Default: `-1`