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

## Extending logging interface and callsite
NLog has a special [Callsite](Callsite-layout-renderer) feature, that allows it to automatically capture the location in source code that performed the logging. This feature has a huge overhead (logging becomes 20 times slower, together with lots of bonus allocations), because the capture of StackTrace and scanning for source location is expensive.

.NET 4.5 introduces the support for [CallerFilePath](https://msdn.microsoft.com/en-us/library/system.runtime.compilerservices.callerfilepathattribute.aspx), which has smaller overhead, but it is currently only supported by [NLog Fluent-API](Fluent-API), that uses "magic" strings to store as [context properties](EventProperties-Layout-Renderer). Official support for this is still missing in the official Logger-interface.

When creating an extension to the NLog Logger-interface, then one will notice the input-parameter `loggerType`. It is used for scanning the captured StackTrace for the source location of the log-statement. If extending the NLog Logger-interface without providing the correct `loggerType`, then [Callsite](Callsite-layout-renderer) will stop working.

In the perfect world then one just have to provide the .NET-Type of the custom logger-interface as value for the `loggerType`-parameter. But the .NET JIT compiler can performing inlining so the custom logger-interface might get inlined completely and the `loggerType` becomes a lie. NLog will trust the `loggerType`, and will attempt to perform filtering based on a type that doesn't exist in the StackTrace (NLog ver. 4.5 will automatically fallback to the default NLog `loggerType`).

### Providing a correct loggerType
Rules for creating a custom logger interface:

- The custom logger interface should be a pure-interface, instead of a class. This will ensure that all log methods becomes virtual and cannot be inlined.
- The custom logger interface implementation should not have multiple levels of inheritance and aggregations. This will ensure that you don't fall into the inline-trap again.
- There should only be two types. The pure-interface-type and the implementation-interface-type. The type provided for the `loggerType` should be the implementation-inteface-type.