Provides asynchronous, buffered execution of target writes. 

Supported in .NET, Silverlight, Compact Framework and Mono.
##Configuration Syntax

```xml
<targets>
  <target xsi:type="AsyncWrapper"
          name="String"
          queueLimit="Integer"
          timeToSleepBetweenBatches="Integer"
          batchSize="Integer"
          overflowAction="Enum">
    <target xsi:type="wrappedTargetType" ...target properties... />
  </target>
</targets>
```
##Parameters
###General Options
_name_ - Name of the target.
###Buffering Options
_queueLimit_ - Limit on the number of requests in the lazy writer thread request queue. Integer Default: `10000`

_timeToSleepBetweenBatches_ - Time in milliseconds to sleep between batches. Integer Default: `50`. When set to `0`, this  will lead to a high CPU usage.

_batchSize_ - Number of log events that should be processed in a batch by the lazy writer thread. Integer Default: 100 (NLog 4.4.2 and newer has Default: 200)

_fullBatchSizeWriteLimit_ - Max number of consecutive full _batchSize_ writes to perform within the same timer event. Integer Default: 5 (Introduced with NLog 4.4.2)

_overflowAction_ - Action to be taken when the lazy writer thread request queue count exceeds the set limit. Default: Discard  
Possible values:  
 * Block - Block until there's more room in the queue.  
 * Discard - Discard the overflowing item.
 * Grow - Grow the queue.

##Remarks


###Async attribute
Asynchronous target wrapper allows the logger code to execute more quickly, by queuing messages and processing them in a separate thread. You should wrap targets that spend a non-trivial amount of time in their `Write()` method with asynchronous target to speed up logging. Because asynchronous logging is quite a common scenario, NLog supports a shorthand notation for wrapping all targets with AsyncWrapper. Just add `async="true"` to the `<targets/>` element in the configuration file.

Example:
```xml
<targets async="true"> 
  ... your targets go here ...
</targets>
```

###AsyncWrapper and `<rules>`

When using the `AsyncWrapper`, do write to the wrapper in your ` <rules>` section! In the following example: do write to 
"target2". If the `<logger>` is writing to "target1", the messages are not written asynchronously!

```xml 
   <targets>
      <target name="target2" xsi:type="AsyncWrapper">
        <target name ="target1" xsi:type="File"
                    fileName="c:/temp/test.log" layout="${message}"
                    keepFileOpen="true" />
      </target>
    <rules>
      <logger name="*" minlevel="Info" writeTo="target2"/>
    </rules>
  </targets> 
```

###Async attribute and AsyncWrapper 
Don't combine the Async attribute and AsyncWrapper. This will only slow down processing and will behave unreliably.

###Async attribute will discard by default
The async attribute is a shorthand for:

```xml
xsi:type="AsyncWrapper overflowAction="Discard" queueLimit="10000" batchSize="100" timeToSleepBetweenBatches="50"
```

So if you write a lot of messages (more then 10000) in a short time, it's possible that messages will be lost. This is intended behavior as keeping all the messages or waiting for all the messages to be written, could have impact on the performance of your program.

If you need all the log messages, do use the AsyncWrapper instead of the async attribute. 

###Asynchronously writing and threads

When messages are written asynchronously, this is done in another thread. Some targets require to write on the main thread and so if asynchronous writing is used, the message get lost.


###BufferingWrapper  and Async
The [BufferingWrapper](https://github.com/NLog/NLog/wiki/BufferingWrapper-target) can write asynchronously by itself. No need to use the async attribute or AsyncWrapper. See [remarks at the BufferingWrapper](https://github.com/NLog/NLog/wiki/BufferingWrapper-target#buffer-and-asynchronously-writing).