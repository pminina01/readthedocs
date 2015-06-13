Log event properties data. 

This has the same implementation as ${event-context}, but the later is deprecated. 

Supported in .NET, Silverlight, Compact Framework and Mono

##Configuration Syntax
```
${event-properties:item=String}
```

##Parameters
###Rendering Options
* **item** - Name of the item. Required.

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
${event-properties:item=MyValue} -- renders "My custom string"
${event-properties:item=TheAnswer} -- renders "42"
```