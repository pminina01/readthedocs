## Use
Targets are used to display, store, or pass log messages to another destination. There are two kinds of target; those that receive and handle the messages, and those that buffer or route the messages to another target. The second group are called 'wrapper' targets. 

NLog supports creating custom targets. For more information, see: [[Extending NLog|Extending-NLog]]

## Targets

### NLog package [![Version](https://img.shields.io/nuget/v/NLog.svg)](https://www.nuget.org/packages/NLog)
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

#### Wrappers
* [AsyncWrapper](AsyncWrapper-target) - Provides asynchronous, buffered execution of target writes.
* [AutoFlushWrapper](AutoFlushWrapper-target) - Causes a flush after each write on a wrapped target.
* [BufferingWrapper](BufferingWrapper-target) - A target that buffers log events and sends them in batches to the wrapped target. Useful in combination with Mail target.
* [FallbackGroup](FallbackGroup-target) - Provides fallback-on-error.
* [FilteringWrapper](FilteringWrapper-target) - Filters log entries based on a condition.
* [ImpersonatingWrapper](ImpersonatingWrapper-target) - Impersonates another user for the duration of the write.
* [LimitingWrapper](LimitingWrapper-target) - Limits number of log events sent to target.
* [PostFilteringWrapper](PostFilteringWrapper-target) - Filters buffered log entries based on a set of conditions that are evaluated on a group of events.
* [RandomizeGroup](RandomizeGroup-target) - Sends log messages to a randomly selected target.
* [RepeatingWrapper](RepeatingWrapper-target) - Repeats each log event the specified number of times.
* [RetryingWrapper](RetryingWrapper-target) - Retries in case of write error.
* [RoundRobinGroup](RoundRobinGroup-target) - Distributes log events to targets in a round-robin fashion.
* [SplitGroup](SplitGroup-target) - Writes log events to all targets.



### NLog.Extended package  [![Version](https://img.shields.io/nuget/v/NLog.Extended.svg)](https://www.nuget.org/packages/NLog.Extended)
* [MSMQ](MSMQ-target) - Writes log message to the specified message queue handled by MSMQ.

### NLog.Web package [![Version](https://img.shields.io/nuget/v/NLog.Web.svg)](https://www.nuget.org/packages/NLog.Web)

* [AspNetTrace](AspNetTrace-target) - Writes log messages to the ASP.NET trace.

#### Wrappers
* [AspNetBufferingWrapper](AspNetBufferingWrapper-target) - Buffers log events for the duration of ASP.NET request and sends them down to the wrapped target at the end of a request.


### NLog.Windows.Forms package [![Version](https://img.shields.io/nuget/v/NLog.Windows.Forms.svg)](https://www.nuget.org/packages/NLog.Windows.Forms)
* [FormControl](FormControl-target) - Logs text to Windows.Forms.Control.Text property control of specified Name.
* [MessageBox](MessageBox-target) - Pops up log messages as message boxes.
* [RichTextBox](https://github.com/NLog/NLog.Windows.Forms/wiki/RichTextBoxTarget) - Log text a Rich Text Box control in an existing or new form.

### NLog.Elmah package [![Version](https://img.shields.io/nuget/v/NLog.Elmah.svg)](https://www.nuget.org/packages/NLog.Elmah)
* [Elmah](Elmah-target) - Logs to Elmah

### External packages
External packages, not maintained by the NLog team.


<!-- PLEASE keep SORTED -->


Package|Version     |Description
-------|------------|------------------------------------------------
[Amazon CloudWatch](https://github.com/aws/aws-logging-dotnet) | [![Version](https://img.shields.io/nuget/v/AWS.Logger.NLog.svg)](https://www.nuget.org/packages/AWS.Logger.NLog) | Writes NLog messages to Amazon CloudWatch Logs (AWS)
[Amazon SNS](https://github.com/Takaloy/NLog.Targets.SNS) | [![Version](https://img.shields.io/nuget/v/NLog.Targets.SNS.svg)](https://www.nuget.org/packages/NLog.Targets.SNS) | Writes NLog messages to Amazon SNS.
[Amazon SQS](https://github.com/aireq/NLog.Targets.SQS) | [![Version](https://img.shields.io/nuget/v/NLog.Targets.SQS.svg)](https://www.nuget.org/packages/NLog.Targets.SQS) | Writes NLog messages to Amazon SQS.
[AzureTableStorage](https://github.com/abkonsta/NLog.Extensions.AzureTableStorage) | [![Version](https://img.shields.io/nuget/v/NLog.Extensions.AzureTableStorage.svg)](https://www.nuget.org/packages/NLog.Extensions.AzureTableStorage/) | Writes NLog messages to Azure TableStorage
[Microsoft ApplicationInsights](https://github.com/Microsoft/ApplicationInsights-dotnet-logging) | [![Version](https://img.shields.io/nuget/v/Microsoft.ApplicationInsights.NLogTarget.svg)](https://www.nuget.org/packages/Microsoft.ApplicationInsights.NLogTarget/) | Writes NLog messages to Microsoft ApplicationInsights
[Elastic Search](https://github.com/ReactiveMarkets/NLog.Targets.ElasticSearch) | [![Version](https://img.shields.io/nuget/v/NLog.Targets.ElasticSearch.svg)](https://www.nuget.org/packages/NLog.Targets.ElasticSearch) | Writes to Elastic Search servers.
[elmah.io](https://github.com/elmahio/elmah.io.nlog)             | [![Version](https://img.shields.io/nuget/v/elmah.io.nlog.svg)](https://www.nuget.org/packages/elmah.io.nlog) | Sends logs to [elmah.io](https://elmah.io). elmah.io is an online service for logging messages in the cloud.
[ExceptionLess](https://github.com/exceptionless/Exceptionless.Net)             | [![Version](https://img.shields.io/nuget/v/Exceptionless.NLog.svg)](https://www.nuget.org/packages/Exceptionless.NLog/) | Writes NLog messages to www.exceptionless.com
[Fluentd](https://github.com/fluent/NLog.Targets.Fluentd) | [![Version](https://img.shields.io/nuget/v/NLog.Targets.Fluentd.svg)](https://www.nuget.org/packages/NLog.Targets.Fluentd/) | Writes NLog messages to Fluentd
[Gelf](https://github.com/2020Legal/NLog.Targets.Gelf)    | [![Version](https://img.shields.io/nuget/v/NLog.Targets.Gelf.svg)](https://www.nuget.org/packages/NLog.Targets.Gelf/) | Writes NLog messages to GrayLog2 - Gelf
[Gelf4NLog](https://github.com/Certegy/Gelf4NLog)             | [![Version](https://img.shields.io/nuget/v/Gelf4NLog.Target.svg)](https://www.nuget.org/packages/Gelf4NLog.Target/) | Writes NLog messages to GrayLog2 - Gelf
[NLog.Gelf](https://github.com/mantasaudickas/NLog.Gelf)             | [![Version](https://img.shields.io/nuget/v/NLog.Gelf.svg)](https://www.nuget.org/packages/NLog.Gelf/) | Writes NLog messages to GrayLog2 - Gelf
[EasyGelf](https://github.com/Pliner/EasyGelf)             | [![Version](https://img.shields.io/nuget/v/EasyGelf.NLog.svg)](https://www.nuget.org/packages/EasyGelf.NLog/) | Writes NLog messages to GrayLog2 - Gelf
[Glimpse](https://github.com/NLog/Glimpse.NLog) | [![Version](https://img.shields.io/nuget/v/Glimpse.NLog.svg)](https://www.nuget.org/packages/Glimpse.NLog) | Show NLog information in [Glimpse](http://getglimpse.com/).
[GrowlNotify](https://github.com/RyanFarley/NLogGrowlNotify)     | [![Version](https://img.shields.io/nuget/v/NLog.Growl.svg)](https://www.nuget.org/packages/NLog.Growl) | Sends logs via [Growl for Windows](http://www.growlforwindows.com/gfw/), a desktop notification system.
[InsightOps](https://github.com/rapid7/r7insight_dotnet)                   | [![Version](https://img.shields.io/nuget/v/r7Insight.nlog.svg)](https://www.nuget.org/packages/r7Insight.nlog) | Writes NLog messages to R7 InsightOps / Logentries
[LiveSwitch](https://www.liveswitch.com) | [![Version](https://img.shields.io/nuget/v/LiveSwitch.nlog.svg)](https://www.nuget.org/packages/LiveSwitch.NLog) | Sends logs via named pipes to a local service that you can monitor in real-time with a UI.
[Loggly](https://github.com/neutmute/nlog-targets-loggly)                   | [![Version](https://img.shields.io/nuget/v/NLog.Targets.Loggly.svg)](https://www.nuget.org/packages/NLog.Targets.Loggly/) | Writes NLog messages to www.loggly.com
[Loupe](https://github.com/GibraltarSoftware/Gibraltar.Agent.NLog2)                   | [![Version](https://img.shields.io/nuget/v/Gibraltar.Agent.NLog4.svg)](https://www.nuget.org/packages/Gibraltar.Agent.NLog4) | Writes NLog messages to Gibraltar www.onloupe.com
[MongoDB](https://github.com/loresoft/NLog.Mongo)                      | [![Version](https://img.shields.io/nuget/v/NLog.Mongo.svg)](https://www.nuget.org/packages/NLog.Mongo) | Writes NLog messages to MongoDB. 
[LiteDB](https://github.com/cccsdh/NLog.LiteDB)                      | [![Version](https://img.shields.io/nuget/v/NLog.LiteDB.svg)](https://www.nuget.org/packages/NLog.LiteDB) | Writes NLog messages to LiteDB. 
[Pushover](https://github.com/RobThree/NLog.Targets.Pushover)    | [![Version](http://img.shields.io/nuget/v/NLog.Targets.Pushover.svg)](https://www.nuget.org/packages/NLog.Targets.Pushover) | Sends logs via [Pushover](https://pushover.net/), an [Android/iOS/Desktop](https://pushover.net/clients) push notification system.
[RabbitMQ](https://github.com/adolya/NLog.RabbitMQ)                 | [![Version](https://img.shields.io/nuget/v/NLog.RabbitMQ.Target.svg)](https://www.nuget.org/packages/Nlog.RabbitMQ.Target/) | Sends logs over a RabbitMQ message broker. It allows you to combine your logs in real time across multiple platforms and systems.
[Raygun](https://github.com/MindscapeHQ/NLog.Raygun)                 | [![Version](https://img.shields.io/nuget/v/NLog.Raygun.svg)](https://www.nuget.org/packages/NLog.Raygun/) | Writes NLog messages to www.raygun.com 
[Redis](https://github.com/richclement/NLog.Redis)                 | [![Version](https://img.shields.io/nuget/v/NLog.Redis.svg)](https://www.nuget.org/packages/NLog.Redis/) | Writes NLog messages to Redis. 
[ReflectInsight](https://github.com/reflectsoftware/reflectinsight-extensions-nlog)                 | [![Version](https://img.shields.io/nuget/v/ReflectSoftware.Insight.Extensions.NLog.svg)](https://www.nuget.org/packages/ReflectSoftware.Insight.Extensions.NLog/) | Writes NLog messages to www.reflectsoftware.com. 
[RavenDB](https://github.com/kentcooper/NLog.Raven)                 | [![Version](https://img.shields.io/nuget/v/NLog.Raven.svg)](https://www.nuget.org/packages/Nlog.Raven/) | Writes NLog messages to [RavenDB](https://ravendb.net/). 
[Sentry](https://github.com/CurtisInstruments/NLog.Targets.Sentry)                 | [![Version](https://img.shields.io/nuget/v/NLog.Targets.Sentry3.svg)](https://www.nuget.org/packages/NLog.Targets.Sentry3) | Writes NLog messages to www.sentry.io 
[Seq](https://github.com/datalust/nlog-targets-seq)                 | [![Version](https://img.shields.io/nuget/v/NLog.Targets.Seq.svg)](https://www.nuget.org/packages/NLog.Targets.Seq) | Writes NLog messages to www.getseq.net
[SignalR](https://github.com/toddmeinershagen/NLog.SignalR)      | [![Version](https://img.shields.io/nuget/v/NLog.SignalR.svg)](https://www.nuget.org/packages/NLog.SignalR/) | Writes NLog messages to a SignalR hub.
[Splunk](https://github.com/AlanBarber/NLog.Targets.Splunk)                   | [![Version](https://img.shields.io/nuget/v/NLog.Targets.Splunk.svg)](https://www.nuget.org/packages/NLog.Targets.Splunk) | Writes NLog messages to Splunk
[Syslog](https://github.com/graffen/NLog.Targets.Syslog)         | [![Version](https://img.shields.io/nuget/v/NLog.Targets.Syslog.svg)](https://www.nuget.org/packages/NLog.Targets.Syslog) | Writes NLog messages to Syslog.

<!-- PLEASE keep SORTED -->

# Writing your own target
NLog supports custom target. For more information, see: [[Extending NLog|Extending-NLog]]
