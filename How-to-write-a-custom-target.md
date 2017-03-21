It’s really easy. Create a class that inherits from `NLog.Targets.TargetWithLayout` and override the `Write()` method. In the body of the method invoke `this.Layout.Render()` to get the message text, then send the text to the destination media.

Don't forget to [register your custom target](Register your custom component)!

### Example
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

### How to pass configuration options to the target?
Consider the above example. There’s a property called “Host” that does just that. Having a public property that sets the required configuration parameters is enough for NLog to use it. Each attribute that you put in the `<target />` definition gets passed to the appropriate public property. NLog takes care of the appropriate conversions necessary so that you can use integer, string, datetime, boolean parameters. Check also [[Properties-constraints-for-custom-extensions]]