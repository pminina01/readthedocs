Exceptions require special treatment in NLog. You need to call the method on the `Logger` class which takes an `Exception` as its first argument. The method name matches the log level. For instance, to log an exception using the `Error` loglevel, do:

    logger.Error(ex, "Oops, an exception occured");

**_Please note_:** the methods have been changed in NLog 4.0. Previous versions expected the exception after the message.

### Example
You typically log exceptions inside a catch handler. An example of logging an exception with the `Error` LogLevel is seen in the following: 
```csharp
try 
{ 
    // some code which may throw 
} 
catch (MyException ex) 
{ 
    logger.Error("Got exception.", ex); //before NLog 4.0
    logger.Error(ex, "Got exception.");  //NLog 4.0

}
```

### Exception Formatting
To write the details of the exception, use the [`${exception}` layout renderer](https://github.com/NLog/NLog/wiki/Exception-Layout-Renderer) in your layout. Depending on the desired output you may want to specify different value for the `format` argument. The following example displays the result of calling `ToString()` on the exception object.

```xml
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