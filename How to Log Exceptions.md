Exceptions require special treatment in NLog. You need to call the method on the `Logger` class which takes an `Exception` as its second argument. The method name matches the log level. For instance, to log an exception using the `Error` loglevel, do:

* `Error("Oops, an exception occured", ex);`

**_Please note_** we have deprecated the `<LogLevel>Exception()` methods, i.e., `ErrorException()` and replaced them with overloads to the standard logging methods. This also includes the `LogException()` method which has been replaced by a `Log()` overload accepting LogLevel, a string, and an exception instance.

### Example
You typically log exceptions inside a catch handler. An example of logging an exception with the `Error` LogLevel is seen in the following: 
```csharp
try 
{ 
    // some code which may throw 
} 
catch (MyException ex) 
{ 
    logger.Error("Got exception.", ex); 
}
```

### Exception Formatting
To write the details of the exception, use the `${exception}` layout renderer in your layout. Depending on the desired output you may want to specify different value for the `format` argument. The following example displays the result of calling `ToString()` on the exception object.
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