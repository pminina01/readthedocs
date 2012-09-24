Exceptions require special treatment in NLog. You need to call method on the Logger class which takes Exception as its second argument. The method name matches the log level:
* `TraceException()`
* `DebugException()`
* `InfoException()`
* `WarnException()`
* `ErrorException()`
* `FatalException()`
* `LogException()` – takes log level as a parameter

You typically call one of these methods in the catch handler:
```csharp
try 
{ 
    // some code which may throw 
} 
catch (MyException ex) 
{ 
    logger.ErrorException("Got exception.", ex); 
}
```

To write the details of the exception, use the ${exception} layout renderer in your layout. Depending on the desired output you may want to specify different value for the “format” argument. The following example displays the result of calling `ToString()` on the exception object.
```csharp
<nlog> 
  <targets> 
    <target name="f" type="File" 
            layout="${longdate} ${message} ${exception:format=tostring}"/> 
  </targets> 
  <rules> 
    <logger name="*" writeTo="f"/> 
  </rules> 
</nlog>
```