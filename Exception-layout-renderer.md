Exception information provided through a call to one of the Logger.*Exception() methods. 

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${exception:innerFormat=String:maxInnerExceptionLevel=Integer:innerExceptionSeparator=String
           :separator=String:format=String}
```

##Parameters
###Rendering Options
* **innerFormat** - Format of the output of inner exceptions. Must be a comma-separated list of exception properties: Message, Type, ShortType, ToString, Method, StackTrace. This parameter value is case-insensitive.

  > This parameter is not supported in:
  > * NLog v1.0 for .NET Compact Framework 1.0
  > * NLog v1.0 for .NET Compact Framework 2.0
  > * NLog v1.0 for .NET Framework 1.0
  > * NLog v1.0 for .NET Framework 1.1
  > * NLog v1.0 for .NET Framework 2.0

* **maxInnerExceptionLevel** - Maximum number of inner exceptions to include in the output. By default inner exceptions are not enabled for compatibility with NLog 1.0.Integer Default: 0

  > This parameter is not supported in:
  > * NLog v1.0 for .NET Compact Framework 1.0
  > * NLog v1.0 for .NET Compact Framework 2.0
  > * NLog v1.0 for .NET Framework 1.0
  > * NLog v1.0 for .NET Framework 1.1
  > * NLog v1.0 for .NET Framework 2.0

* **innerExceptionSeparator** - Separator between inner exceptions.
  > This parameter is not supported in:
  > * NLog v1.0 for .NET Compact Framework 1.0
  > * NLog v1.0 for .NET Compact Framework 2.0
  > * NLog v1.0 for .NET Framework 1.0
  > * NLog v1.0 for .NET Framework 1.1
  > * NLog v1.0 for .NET Framework 2.0

* **separator** - Separator used to concatenate parts specified in the Format. Default:
* **format** - Format of the output. Must be a comma-separated list of exception properties: Message, Type, ShortType, ToString, Method, StackTrace, Data. This parameter value is case-insensitive.

##More Info and Examples
For more information, see [How to properly log exceptions](How-to-log-exceptions).
