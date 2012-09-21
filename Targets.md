##Use
Targets are used to display, store, or pass log messages to another destination. There are two kinds of target; those that receive and handle the messages, and those that buffer or route the messages to another target. The second group are called 'wrapper' targets.

##Supported Targets
* AspNetTrace - Writes log messages to the ASP.NET trace.
* AspResponse - Outputs log messages through the ASP Response object.
* Chainsaw - Sends log messages to the remote instance of Chainsaw application from log4j.
* ColoredConsole - Writes log messages to the console with customizable coloring.
* Console - Writes log messages to the console.
* Database - Writes log messages to the database using an ADO.NET provider.
* Debug - Mock target - useful for testing.
* Debugger - Writes log messages to the attached managed debugger.
* EventLog - Writes log message to the Event Log.
* File - Writes log messages to one or more files.
* FormControl - Logs text to Windows.Forms.Control.Text property control of specified Name.
* LogReceiverService - Sends log messages to a NLog Receiver Service (using WCF or Web Services).
* Mail - Sends log messages by email using SMTP protocol.
* Memory - Writes log messages to an ArrayList in memory for programmatic retrieval.
* MessageBox - Pops up log messages as message boxes.
* MethodCall - Calls the specified static method on each log message and passes contextual parameters to it.
* MSMQ - Writes log message to the specified message queue handled by MSMQ.
* Network - Sends log messages over the network.
* NLogViewer - Sends log messages to the remote instance of NLog Viewer.
* Null - Discards log messages. Used mainly for debugging and benchmarking.
* OutputDebugString - Outputs log messages through the OutputDebugString() Win32 API.
* PerfCounter - Increments specified performance counter on each write.
* RichTextBox - Log text a Rich Text Box control in an existing or new form.
* Trace - Sends log messages through System.Diagnostics.Trace.
* WebService - Calls the specified web service on each log message.

##Wrapper Targets
* AspNetBufferingWrapper - Buffers log events for the duration of ASP.NET request and sends them down to the wrapped target at the end of a request.
* AsyncWrapper - Provides asynchronous, buffered execution of target writes.
* AutoFlushWrapper - Causes a flush after each write on a wrapped target.
* BufferingWrapper - A target that buffers log events and sends them in batches to the wrapped target.
* FallbackGroup - Provides fallback-on-error.
* FilteringWrapper - Filters log entries based on a condition.
* ImpersonatingWrapper - Impersonates another user for the duration of the write.
* PostFilteringWrapper - Filters buffered log entries based on a set of conditions that are evaluated on a group of events.
* RandomizeGroup - Sends log messages to a randomly selected target.
* RepeatingWrapper - Repeats each log event the specified number of times.
* RetryingWrapper - Retries in case of write error.
* RoundRobinGroup - Distributes log events to targets in a round-robin fashion.
* SplitGroup - Writes log events to all targets.

##Custom Targets
[RabbitMQ target](https://github.com/haf/NLog.RabbitMQ) ([NuGet](http://nuget.org/packages/NLog.RabbitMQ)) - sends logs over a RabbitMQ message broker. It allows you to combine your logs in real time across multiple platforms and systems.

NLog supports custom target. For more information, see: [How to write a Target](How to write a Target)