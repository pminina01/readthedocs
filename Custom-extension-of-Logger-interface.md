## Introduction
There can be different reasons for extending the NLog logging interface:

* Extend logging interface to automatically add relevant [context properties](EventProperties-Layout-Renderer) when logging.
* Create an abstract interface to avoid direct NLog dependency.

## Abstract Interface Libraries
There already exists several libraries that implements an abstract interface:

* [Microsoft.System.Diagnostics.Trace](https://msdn.microsoft.com/en-us/library/system.diagnostics.trace.aspx) ([Setup NLogTraceListener](Send-System-Diagnostic-(Trace)-to-NLog))
* [Common Logging](http://net-commons.github.io/common-logging/)
* [LibLog](https://github.com/damianh/LibLog/wiki) - Useful for shared libraries
* [Microsoft.Extensions.Logging](https://github.com/aspnet/Logging)

## Extended logging interface
There are two ways to extend the NLog Logger.

- Inherit from the NLog Logger and add your own custom extensions.
- Create a custom wrapper around the NLog Logger and forward the logevents to the NLog Logger.

## Custom Wrapper and callsite
NLog has a special [Callsite](Callsite-layout-renderer) feature, that allows it to automatically capture the location in source code that performed the logging. This feature has a huge overhead (logging becomes 20 times slower, together with lots of bonus allocations), because the capture of StackTrace and scanning for source location is expensive.

.NET 4.5 introduces the support for [CallerFilePath](https://msdn.microsoft.com/en-us/library/system.runtime.compilerservices.callerfilepathattribute.aspx), which has smaller overhead, but it is currently only supported by [NLog Fluent-API](Fluent-API), that uses "magic" strings to store as [context properties](EventProperties-Layout-Renderer). Official support for this is still missing in the official Logger-interface.

When creating a custom wrapper around the NLog Logger-interface, then the callsite logic will think the custom wrapper is the origin of the log-statement. To avoid this then the custom wrapper should only call this NLog Logger method:

```c#
Logger.Log(Type wrapperType, LogEventInfo logEvent)
```

The custom wrapper should provide its own Type as wrapperType, and then the callsite logic will not see the custom wrapper as being the origin of the log-statement. If extending the NLog Logger-interface without providing the correct `loggerType`, then [Callsite](Callsite-layout-renderer) will stop working.