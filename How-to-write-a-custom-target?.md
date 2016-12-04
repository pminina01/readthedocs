It’s really easy. Create a class that inherits from `NLog.Targets.TargetWithLayout` and override the `Write()` method. In the body of the method invoke `this.Layout.Render()` to get the message text, then send the text to the destination media.




###Example
This is a skeleton target that writes messages to the specified host. Compile using:

`csc.exe /t:library /out:MyAssembly.dll /r:NLog.dll MyFirstTarget.cs`
```csharp
using NLog;
using NLog.Config;
using NLog.Targets;
 
namespace MyNamespace 
{ 
    [Target("MyFirst")] 
    public sealed class MyFirstTarget: TargetWithLayout 
    { 
        public MyFirstTarget()
        {
            this.Host = "localhost";
        }
 
        [RequiredParameter] 
        public string Host { get; set; }
 
        protected override void Write(LogEventInfo logEvent) 
        { 
            string logMessage = this.Layout.Render(logEvent); 
 
            SendTheMessageToRemoteHost(this.Host, logMessage); 
        } 
 
        private void SendTheMessageToRemoteHost(string host, string message) 
        { 
            // TODO - write me 
        } 
    } 
}
```

###How to pass configuration options to the target?
Consider the above example. There’s a property called “Host” that does just that. Having a public property that sets the required configuration parameters is enough for NLog to use it. Each attribute that you put in the `<target />` definition gets passed to the appropriate public property. NLog takes care of the appropriate conversions necessary so that you can use integer, string, datetime, boolean parameters.

##How to write a custom layout renderer?
Create a class that inherits from `NLog.LayoutRenderers.LayoutRenderer`, set the `[LayoutRenderer("your-name"]` on the class and override the `Append(StringBuilder builder, LogEventInfo logEvent)` method. 
Invoke in this method `builder.Append(..)` to render your custom layout renderer.

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
- `${hello-world:true:config2=abc:config1=yes}` - all the three properties set.