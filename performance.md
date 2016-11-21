NLog is written with performance in mind. So writing a lot of messages should have no significant impact. For this reason also NLog minimal parses your messages. 

There are some things to know for the optimal performance:

- Don't use `string.format` but pass the arguments to the log method. 
- Don't write with multiple threads to multiple files. 
- If even the small overhead of NLog is too much, use "Conditional logging", as described below.



###Conditional logging

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


##File Logging Performance
Single process applications (in single AppDomain). Can optimize performance by configuring the FileTarget attributes _keepFileOpen_ = True and _concurrentwrites_ = False. See also [FileTarget - Performance](../wiki/File-target#performance-tuning-options)

To avoid the blocking file write operation, then one can consider to wrap the FileTarget within a [AsyncWrapper](../wiki/AsyncWrapper-target). This will also optimize the writing against the disk, as it will be done in batches. Be careful as the default behavior is to discard log operations if they come fast. It is recommended to set

-  _overflowAction_ = Block 
- _queueLimit_ = 10000, 
- _batchSize_ = 500 and 
- _timeToSleepBetweenBatches_ = 50. 

For optimal performance set _timeToSleepBetweenBatches_ = 0, though it will make it write in smaller batches and give higher priority to logging when high activity.