NLog is written with performance in mind. So writing a lot of messages should have no significant impact. For this reason also NLog minimal parses your messages. 

There are some things to know for the optimal performance:

- Don't use `string.format` but pass the arguments to the log method. 
- Don't write with multiple threads to multiple files. 
- If even the small overhead of NLog is too much, use "Conditional logging", as described below.

### Deferring message-formatting

The goal is to defer the message-formatting so it becomes async. The async message-formatting requires that all parameters are immutable. To ensure that they don't change after having called the Logger (Ex logging an object and disposing the object afterwards should not log a disposed object).

The NLog Logger (During the creation of LogEventInfo) checks whether all parameters are immutable / primitive. If one is complex-object, then message-formatting is not deferred.
When having more than 5 parameters then it will skip the performance optimization, because checking the immutable state of the parameters has a cost.

### Conditional logging

In extreme cases logging could affect the performance of your application. There is a small overhead when writing a lot of log messages.
Starting of NLog 4.0 it’s possible to only include the `Trace` and `Debug` call with a debug release. 
Instead of:

```c#
Logger.Trace("entering method {0}", methodname);
```

Use:

```c#
Logger.ConditionalTrace("entering method {0}", methodname);
```

This call will be removed by the .Net compiler if the DEBUG conditional compilation symbol is not set – default on a release build.


## File Logging Performance
Single process applications (in single AppDomain) can optimize performance by configuring the FileTarget attributes:
- _keepFileOpen_ = True
- _concurrentwrites_ = False

See also [FileTarget - Performance](../wiki/File-target#performance-tuning-options)

To avoid the blocking file write operation, then one can consider to wrap the FileTarget within a [AsyncWrapper](../wiki/AsyncWrapper-target) (Very important if using _keepFileOpen_ = False). This will also optimize the writing against the disk, as it will be done in batches. Be careful as the default behavior is to discard log operations if they come fast. It is recommended to set:

- _overflowAction_ = Block 
- _timeToSleepBetweenBatches_ = 0

This can be done for all registered targets by placing this as first element inside the `<targets>` section:

```xml
<default-wrapper xsi:type="AsyncWrapper" timeToSleepBetweenBatches="0" overflowAction="Block" />
```