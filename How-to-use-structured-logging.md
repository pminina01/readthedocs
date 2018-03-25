NLog 4.5 introduces structured logging - also called message templates and structural logging. This document describes how to use structured logging. The implementation in NLog uses the message templates rules and so it's also recommend to check: https://messagetemplates.org/


# Why structured logging
Structured logging makes it easier to store and query log-events, as the logevent message-template and message-parameters are preserved, instead of just transforming them into a formatted message.

The normal .NET `string.Format(...)` will only accept input strings like this:

```c#
logger.Info("Logon by user:{0} from ip_address:{1}", "Kenny", "127.0.0.1");
logger.Debug("Shopitem:{0} added to basket by user:{1}", "Jacket", "Kenny");
```

When storing these log-events in a database (or somewhere else), then it can be difficult to query all actions performed by a certain user. Also it could be hard to group similar events. 

The workaround would then be to perform RegEx-queries to recognize logevent messages and convert them into a more structured format, and register which parameter index is the user. The RegEx might even have to extract the needed details from the formatted message, making it even more fragile. Maintaining these RegEx-queries can become rather cumbersome.

Further history: [messagetemplates.org](http://messagetemplates.org/)

# Using structured logging
NLog has always supported log-event metadata called [event-properties](EventProperties-Layout-Renderer), but it requires a little effort to generate a log-event with properties.

NLog 4.5 makes it a easier to capture and preserve log-event-properties, so they can be easily processed by the NLog destination target:

```c#
logger.Info("Logon by {user} from {ip_address}", "Kenny", "127.0.0.1"); // Logon by "Kenny" from "127.0.0.1"
logger.Debug("{shopitem} added to basket by {user}", new { Id=6, Name = "Jacket", Color = "Orange" }, "Kenny");
```

Any NLog destination target that is able to handle log-event-properties will automatically experience the benefit of doing structured logging.


## Formatting of the message
The formatting of message depends on the datatype of the parameters.

Example:
```c#
logger.Info("Order {orderid} created for {user}", 42, "Kenny");
```

Will be formatted as:

`Order 42 created for "Kenny"`

The formatting is controlled by the datatype of the parameter:
- string: surrounded with double quotes, e.g `"hello"`
- number: no quotes
- null: printed as `NULL`
- list/ienumerable/array: `"item1", "item2"` 
- dictionary: `"key1"="value1", "key2"="value2"`
- objects: `ToString()` 

It's possible to control formatting by preceding `@` or `$`:

- `@` will format the object as JSON
- `$` forces `ToString()`


### Examples



```c#
Object o = null;

logger.Info("Test {value1}", o); // null case. Result:  Test NULL
logger.Info("Test {value1}", new DateTime(2018,03, 25)); // datetime case. Result:  Test 25-3-2018 00:00:00 (locale TString)
logger.Info("Test {value1}", new List<string> { "a", "b" }); // list of strings. Result: Test "a", "b"
logger.Info("Test {value1}", new[] { "a", "b" }); // array. Result: Test "a", "b"
logger.Info("Test {value1}", new Dictionary<string, int> { { "key1", 1 }, { "key2", 2 } }); // dict. Result:  Test "key1"=1, "key2"=2

var order = new Order
{
    OrderId = 2,
    Status = OrderStatus.Processing
};

logger.Info("Test {value1}", order); // object Result:  Test MyProgram.Program+Order
logger.Info("Test {@value1}", order); // object Result:  Test {"OrderId":2, "Status":"Processing"}
logger.Info("Test {value1}", new { OrderId = 2, Status = "Processing"}); // anomynous object. Result: Test { OrderId = 2, Status = Processing }
logger.Info("Test {@value1}", new { OrderId = 2, Status = "Processing"}); // anomynous object. Result:Test {"OrderId":2, "Status":"Processing"}

```




## Capture parameters

The parameters will be serialized to the message (see formatting) and could be retrieved as object with 

`${event-properties}` or `${all-event-properties}`, for example:

```xml
    <target xsi:type="File" name="jsonFile" fileName="c:\temp\nlog-json-${shortdate}.log">

      <layout xsi:type="JsonLayout">
        <attribute name="time" layout="${longdate}" />
        <attribute name="level" layout="${level:upperCase=true}"/>
        <attribute name="message" layout="${message}" />
        <attribute name="orderid" layout="${event-properties:orderid}" />
      </layout>

    </target>
```

For the JSON layout you could also use: `includeAllProperties`:

```xml
    <target xsi:type="File" name="jsonFile" fileName="c:\temp\nlog-json-${shortdate}.log">

      <layout xsi:type="JsonLayout" includeAllProperties="true">
        <attribute name="time" layout="${longdate}" />
        <attribute name="level" layout="${level:upperCase=true}"/>
        <attribute name="message" layout="${message}" />
      </layout>

    </target>

```

In code you could use `LogEventInfo.MessageTemplateParameters`

# NLog Layout Support
The [Json Layout](JsonLayout) and [Log4JXml Layout](Log4JXmlEventLayout) already has builtin support for [event-properties](EventProperties-Layout-Renderer), and automatically supports structured logging. Just configure the setting `includeAllProperties="true"`

NLog 4.5 adds support for rendering the raw message-template, instead of just the formatted message:
* [$(message:raw=true)](Message-Layout-Renderer)

NLog 4.5 extends the following NLog LayoutRenderers with support for serializing with property reflection into JSON when `format="@"`

* [$(event-properties)](EventProperties-Layout-Renderer)
* [$(all-event-properties)](All-Event-Properties-Layout-Renderer)
* [$(exception)](Exception-Layout-Renderer)
* [$(gdc)](Gdc-Layout-Renderer) - Global Context
* [$(mdc)](Mdc-Layout-Renderer) - Thread Context
* [$(mdlc)](Mdlc-Layout-Renderer) - Async Context

# NLog Target Support
Any NLog destination target that handles [event-properties](EventProperties-Layout-Renderer) will be able to take advantage from structured logging.

These NLog targets already supports structured logging:

* [NLogViewer Target](NLogViewer-target) has automatic support by using the [Log4JXml Layout](Log4JXmlEventLayout).
* [WebService Target](WebService-target) has automatic support by using the [Json Layout](JsonLayout) for JSON-post.

There are already many custom NLog targets, that provides the ability to store log-events in central storage, and allowing a Web-Application to query the log-events along with their event-properties. These targets will automatically benefit from doing structured logging, and allow the Web-Application to perform effective queries.

# Disabling Structured Logging
NLog will by default attempt to parse log-events as structured log-events. This gives a minor overhead, that will not be noticable by most.

It is possible to disable that NLog should not attempt to parse log-events as structured log-events with this xml-setting:

```xml
<nlog parseMessageTemplates="false">
    ...
</nlog>
```


## Advanced

### I need a custom formatter

Create a new class that `NLog.IValueFormatter` and set ` NLog.Config.ConfigurationItemFactory.Default.ValueFormatter`

### I like to use Json.NET for creating JSON.

You need a custom `NLog.IJsonConverter` and set `NLog.Config.ConfigurationItemFactory.Default.JsonConverter`

e.g.

```c#
    internal class JsonNetSerializer : NLog.IJsonConverter
    {
        readonly JsonSerializerSettings _settings;

        public JsonNetSerializer()
        {
           _settings = new JsonSerializerSettings
                {
                    Formatting = Formatting.Indented,
                    ReferenceLoopHandling = ReferenceLoopHandling.Ignore
                };
        }

        /// <summary>Serialization of an object into JSON format.</summary>
        /// <param name="value">The object to serialize to JSON.</param>
        /// <param name="builder">Output destination.</param>
        /// <returns>Serialize succeeded (true/false)</returns>
        public bool SerializeObject(object value, StringBuilder builder)
        {
            try
            {
                var jsonSerializer = JsonSerializer.CreateDefault(_settings);
                var sw = new System.IO.StringWriter(builder, System.Globalization.CultureInfo.InvariantCulture);
                using (var jsonWriter = new JsonTextWriter(sw))
                {
                    jsonWriter.Formatting = jsonSerializer.Formatting;
                    jsonSerializer.Serialize(jsonWriter, value, null);
                }
            }
            catch (Exception e)
            {
                NLog.Common.InternalLogger.Error(e, "Error when custom JSON serialization");
                return false;
            }
            return true;
        }
    }
```

### Combine indexed and structured logging

e.g. logging `"Hello {0} with {Message}"`

For backward compatibility (and performance), then NLog will by default skip full parsing if it detects the first parameter as being positional index.

When `parseMessageTemplates='true'` then NLog will always parse all parameters, and if one is non-numeric, then all the parameters will be treated as structured parameters. Mixing and numeric and structured parameters is not recommended, as it hurts performance (backtrack) and numeric parameters are most of the time not so descriptive.

### Parameter Names

The Names of the parameters should be unique


### I just need the template

e.g. `Order {orderId}`

Use `${message:raw=true}`