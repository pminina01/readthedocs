Log event context data. 

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${event-context:item=String}
```

##Parameters
###Rendering Options
* _item_ - Name of the item. Required.

##Example
In C# class, create an event and add an element to the Properties dictionary (or the deprecated Context dictionary):

```csharp
...
Logger log = LogManager.GetCurrentClassLogger();
LogEventInfo theEvent = new LogEventInfo(LogLevel.Debug, "", "Pass my custom value");
theEvent.Properties["MyValue"] = "My custom string";
// deprecated
theEvent.Context["TheAnswer"] = 42;
log.Log(theEvent);
...
```

and in your NLog.config file:

```
${event-context:item=MyValue} -- renders "My custom string"
${event-context:item=TheAnswer} -- renders "42"
```