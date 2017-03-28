Log event properties data. 

This has the same implementation as `${event-context}`, but the latter is deprecated. 

Supported in .NET, Silverlight, Compact Framework and Mono

To log all properties, use [`${all-event-properties}`](All-Event-Properties-Layout-Renderer).

## Configuration Syntax
```
${event-properties:item=String:culture=String:format=String}
```

## Parameters
### Rendering Options
* **item** - Name of the item. Required.
* **culture** - The culture used for rendering. Introduced in NLog 4.1. Default value is `CultureInfo.InvariantCulture`
* **format** - Format for conversion from object to string. Introduced in NLog 4.1. 


## Example
In C# class, create an event and add an element to the Properties dictionary (or the deprecated Context dictionary):
```csharp
...
Logger log = LogManager.GetCurrentClassLogger();
LogEventInfo theEvent = new LogEventInfo(LogLevel.Debug, "", "Pass my custom value");
theEvent.Properties["MyValue"] = "My custom string";
theEvent.Properties["MyDateTimeValue"] = new DateTime(2015, 08, 30, 11, 26, 50);
theEvent.Properties["MyDateTimeValueWithCulture"] = new DateTime(2015, 08, 30, 11, 26, 50);
theEvent.Properties["MyDateTimeValueWithCultureAndFormat"] = new DateTime(2015, 08, 30, 11, 26, 50);
log.Log(theEvent);
...
```

and in your NLog.config file:

```
${event-properties:item=MyValue} -- renders "My custom string"
${event-properties:item=TheAnswer} -- renders "42"
${event-properties:MyDateTimeValue:format=yyyy-M-dd}"; -- renders "2015-8-30"
${event-properties:MyDateTimeValueWithCulture:culture=en-US} -- renders "8/30/2015 11:26:50 AM"
${event-properties:MyDateTimeValueWithCultureAndFormat:format=yyyy-M-dd HH:mm:ss:culture=en-US} -- renders "2015-8-30 11:26:50"
```