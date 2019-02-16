Log event all context data. 

Introduced in NLog v4.0.

Supported in .NET, Silverlight and Mono.

To log one property, use [`${event-properties}`](https://github.com/NLog/NLog/wiki/EventProperties-Layout-Renderer).

## Configuration Syntax

```xml
${all-event-properties:format=String:separator=String:includeCallerInformation=Boolean}
```

## Parameters

### Rendering Options

* **format** - How key/value pairs will be formatted. The placeholder used to define placement of the key is, `[key]`, and the placeholder for value is, `[value]`.
  * Default value: `[key]=[value]`
* **separator** - The string that will be used to separate key/value pairs.
  * Default value: `, `
* **includeCallerInformation** - Also render the caller information attributes? .Net 4.5 required.
  * Default value: `false`