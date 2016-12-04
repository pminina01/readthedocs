Since NLog 4.4 there are two ways to create a custom layout renderer.

You could write a custom layout with one lambda function - it will be registed intermediately, or you could write a class with is easier to share acros projects. 

## Lamba Function
Introducted in NLog 4.4

For some cases it's easier to write a lambda function. 

The lambda function will accept 1 or 2 parameters and should return a `string`.

- 1 parameter: the `logEventInfo`.
- 2 parameters: `logEventInfo` and the current NLog config.

Examples 
```c#
//register ${text-fixed}
LayoutRenderer.Register("test-fixed", (logEvent) => "2");

//register ${trace-identifier}
LayoutRenderer.Register("trace-identifier", (logEvent) => HttpContext.Current.TraceIdentifier);

//Using logEventInfo, ${message-length}
LayoutRenderer.Register("message-length", (logEvent) => logEvent.Message.Length);

//Using config, ${targetCount}
LayoutRenderer.Register("targetCount",(logEvent, config) => config.AllTargets.Count);
```




## Class
Create a class that inherits from `NLog.LayoutRenderers.LayoutRenderer`, set the `[LayoutRenderer("your-name"]` on the class and override the `Append(StringBuilder builder, LogEventInfo logEvent)` method. 
Invoke in this method `builder.Append(..)` to render your custom layout renderer.

Don't forget to [register your custom layout renderer](Register your custom component)!

###Example
We create a `${hello-world}` layout renderer, which renders..."hello world!".

```c#
[LayoutRenderer("hello-world")]
public class HelloWorldLayoutRenderer : LayoutRenderer
{
    protected override void Append(StringBuilder builder, LogEventInfo logEvent)
    {
        builder.Append("hello world!");
    }
}


```

###How to pass configuration options to the layout render?
Just create public properties on the Layout Renderer. The properties could be decorated with the `[RequiredParameter]` and `[DefaultParameter]` attributes. The `[DefaultParameter]` is can be passed to the layout renderer without using the name.



for example:

```c#
[LayoutRenderer("hello-world")]
public class HelloWorldLayoutRenderer : LayoutRenderer
{
        /// <summary>
        /// I'm not required or default
        /// </summary>
        public string Config1 { get; set; }

        /// <summary>
        /// I'm required
        /// </summary>
        [RequiredParameter]
        public string Config2 { get; set; }

        /// <summary>
        /// I'm the default parameter. You can set me as required also.
        /// </summary>
        [DefaultParameter]
        public bool Caps {get;set;}

```

Example usages

- `${hello-world}` - raises exception: required parameter Config2 isn't set
- `${hello-world:Config2=abc}` - OK, Config2 property set
- `${hello-world:true:config2=abc}` - default parameter (Caps) set to `true`
- `${hello-world:true:config2=abc:config1=yes}` - all the three properties se