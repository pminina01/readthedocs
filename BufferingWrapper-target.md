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

##Remarks

###Buffer and asynchronously writing

If `slidingTimeout` is set to `true`, then the messages are written asynchronously. There is then no need to use this target in combination with the `async` attribute or the [AsyncWrapper](https://github.com/NLog/NLog/wiki/AsyncWrapper-target). Using the `slidingTimeout` is preferred over the `async` attribute and AsyncWrapper. Combining both can lead to lost messages.

When messages are written asynchronously, this is done in another thread. Some targets require to write on the main thread and so if asynchronous writing is used, the message get lost.
