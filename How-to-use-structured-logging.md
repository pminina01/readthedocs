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


## Formatting 
The formatting of message templates parameters depends on the datatype (and not just `ToString`):

Example:

`logger.Info("Order {orderid} created for {user}", 42, "Kenny");`

Will be formatted as:

`Order 42 created for "Kenny"`

The formatting is controlled by the datatype of the parameter:
- `string`: surrounded with quotes
- `number`: no quotes
- `null`: printed as `NULL`
- `list/ienumerable`: comma separated, without `[` and `]`
- `dictionary`: "key1"="value1", "key2"="value2"
- `objects`: toString by default

It's possible to prefix the hole names with the operator `@` or `$`:

- '@' will destructure the object into JSON (Supports object property reflection)
- `$` will force toString

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