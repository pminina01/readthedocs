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
_queueLimit_ - Limit on the number of requests in the lazy writer thread request queue. Integer Default: 10000

_timeToSleepBetweenBatches_ - Time in milliseconds to sleep between batches. Integer Default: 50

_batchSize_ - Number of log events that should be processed in a batch by the lazy writer thread. Integer Default: 100

_overflowAction_ - Action to be taken when the lazy writer thread request queue count exceeds the set limit. Default: Discard  
Possible values:  
 * Block - Block until there's more room in the queue.  

 * Discard - Discard the overflowing item.
 * Grow - Grow the queue.

##Remarks
Asynchronous target wrapper allows the logger code to execute more quickly, by queueing messages and processing them in a separate thread. You should wrap targets that spend a non-trivial amount of time in their Write() method with asynchronous target to speed up logging. Because asynchronous logging is quite a common scenario, NLog supports a shorthand notation for wrapping all targets with AsyncWrapper. Just add async="true" to the <targets/> element in the configuration file.
```
<targets async="true"> 
  ... your targets go here ...
</targets>