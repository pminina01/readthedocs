##Use
Targets are used to display, store, or pass log messages to another destination. There are two kinds of target; those that receive and handle the messages, and those that buffer or route the messages to another target. The second group are called 'wrapper' targets. 

NLog supports creating custom targets. For more information, see: [Extending NLog](Extending NLog)

##Targets

###NLog package [![Version](https://img.shields.io/nuget/v/NLog.svg)](https://www.nuget.org/packages/NLog)
* [AspResponse](AspResponse-target) - Outputs log messages through the ASP Response object.
* [Chainsaw](Chainsaw-target) - Sends log messages to the remote instance of Chainsaw application from log4j.
* [ColoredConsole](ColoredConsole-target) - Writes log messages to the console with customizable coloring.
* [Console](Console-target) - Writes log messages to the console.
* [Database](Database-target) - Writes log messages to the database using an ADO.NET provider.
* [Debug](Debug-target) - Mock target - useful for testing.
* [Debugger](Debugger-target) - Writes log messages to the attached managed debugger.
* [EventLog](EventLog-target) - Writes log message to the Event Log.
* [File](File-target) - Writes log messages to one or more files.
* [LogReceiverService](LogReceiverService-target) - Sends log messages to a NLog Receiver Service (using WCF or Web Services).
* [Mail](Mail-target) - Sends log messages by email using SMTP protocol.
* [Memory](Memory-target) - Writes log messages to an ArrayList in memory for programmatic retrieval.
* [MethodCall](MethodCall-target) - Calls the specified static method on each log message and passes contextual parameters to it.
* [Network](Network-target) - Sends log messages over the network.
* [NLogViewer](NLogViewer-target) - Sends log messages to the remote instance of NLog Viewer.
* [Null](Null-target) - Discards log messages. Used mainly for debugging and benchmarking.
* [OutputDebugString](OutputDebugString-target) - Outputs log messages through the OutputDebugString() Win32 API.
* [PerfCounter](PerfCounter-target) - Increments specified performance counter on each write.
* [Trace](Trace-target) - Sends log messages through System.Diagnostics.Trace.
* [WebService](WebService-target) - Calls the specified web service on each log message.

###NLog.Extended package  [![Version](https://img.shields.io/nuget/v/NLog.Extended.svg)](https://www.nuget.org/packages/NLog.Extended)
* [MSMQ](MSMQ-target) - Writes log message to the specified message queue handled by MSMQ.

###NLog.Web package [![Version](https://img.shields.io/nuget/v/NLog.Web.svg)](https://www.nuget.org/packages/NLog.Web)

* [AspNetTrace](AspNetTrace-target) - Writes log messages to the ASP.NET trace.


###NLog.Windows.Forms package [![Version](https://img.shields.io/nuget/v/NLog.Windows.Forms.svg)](https://www.nuget.org/packages/NLog.Windows.Forms)
* [FormControl](FormControl-target) - Logs text to Windows.Forms.Control.Text property control of specified Name.
* [MessageBox](MessageBox-target) - Pops up log messages as message boxes.
* [RichTextBox](RichTextBox-target) - Log text a Rich Text Box control in an existing or new form.



###External packages
External packages, not maintained the NLog team.

 * [RabbitMQ target](https://github.com/haf/NLog.RabbitMQ) - sends logs over a RabbitMQ message broker. It allows you to combine your logs in real time across multiple platforms and systems.
 [![Version](https://img.shields.io/nuget/v/NLog.RabbitMQ.svg)](https://www.nuget.org/packages/NLog.RabbitMQ)
 * [GrowlNotify target](https://github.com/RyanFarley/NLogGrowlNotify) – sends logs via [Growl for Windows](http://www.growlforwindows.com/gfw/), a desktop notification system.
[![Version](https://img.shields.io/nuget/v/NLog.Growl.svg)](https://www.nuget.org/packages/NLog.Growl)
 * [Pushover target](https://github.com/RobThree/NLog.Targets.Pushover) – sends logs via [Pushover](https://pushover.net/), an [Android/iOS/Desktop](https://pushover.net/clients) push notification system.
[![Version](http://img.shields.io/nuget/v/NLog.Targets.Pushover.svg)](https://www.nuget.org/packages/NLog.Targets.Pushover)
 * [SignalR target](https://github.com/toddmeinershagen/NLog.SignalR) - Custom NLog target for sending log events to a SignalR hub.
[![Version](https://img.shields.io/nuget/v/NLog.SignalR.svg?style=flat)](https://www.nuget.org/packages/NLog.SignalR/)
[![Download Total](https://img.shields.io/nuget/dt/NLog.SignalR.svg?style=flat)](https://www.nuget.org/packages/NLog.SignalR/)

##Wrapper Targets

###NLog package [![Version](https://img.shields.io/nuget/v/NLog.svg)](https://www.nuget.org/packages/NLog)
* [AsyncWrapper](AsyncWrapper-target) - Provides asynchronous, buffered execution of target writes.
* [AutoFlushWrapper](AutoFlushWrapper-target) - Causes a flush after each write on a wrapped target.
* [BufferingWrapper](BufferingWrapper-target) - A target that buffers log events and sends them in batches to the wrapped target. Useful in combination with Mail target.
* [FallbackGroup](FallbackGroup-target) - Provides fallback-on-error.
* [FilteringWrapper](FilteringWrapper-target) - Filters log entries based on a condition.
* [ImpersonatingWrapper](ImpersonatingWrapper-target) - Impersonates another user for the duration of the write.
* [PostFilteringWrapper](PostFilteringWrapper-target) - Filters buffered log entries based on a set of conditions that are evaluated on a group of events.
* [RandomizeGroup](RandomizeGroup-target) - Sends log messages to a randomly selected target.
* [RepeatingWrapper](RepeatingWrapper-target) - Repeats each log event the specified number of times.
* [RetryingWrapper](RetryingWrapper-target) - Retries in case of write error.
* [RoundRobinGroup](RoundRobinGroup-target) - Distributes log events to targets in a round-robin fashion.
* [SplitGroup](SplitGroup-target) - Writes log events to all targets.

###NLog.Web package [![Version](https://img.shields.io/nuget/v/NLog.Web.svg)](https://www.nuget.org/packages/NLog.Web)
* [AspNetBufferingWrapper](AspNetBufferingWrapper-target) - Buffers log events for the duration of ASP.NET request and sends them down to the wrapped target at the end of a request.



#Writing your own target
NLog supports custom target. For more information, see: [Extending NLog](Extending NLog)