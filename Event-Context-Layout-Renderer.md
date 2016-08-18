Log event property data. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax

```
${event-properties:item=MyValue}
```

Note that this syntax replaces the deprecated `${event-context}` syntax.

## Parameters

### Rendering Options

* _item_ - Name of the item (required)

## Example

In your C# code, create an event and add an element to the `Properties` dictionary (or the deprecated `Context` dictionary):

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

And in your `NLog.config` file:

```plain
${event-properties:item=MyValue}   -- renders "My custom string"
${event-properties:item=TheAnswer} -- renders "42"
```