##Why would I want to write a Target?
If you want to write your log messages to a non-standard output (for example to some management console) or when you need a protocol which is not supported by NLog, you need to write a custom Target.

##How to write a target?
It’s really easy. Create a class that inherits from NLog.Targets.TargetWithLayout and override the Write() method. In the body of the method invoke this.Layout.Render() to get the message text, then send the text to the destination media.

##Example
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

##How to use the newly created target?
It’s easy. Just put the target in a DLL and reference it from the the config file using the `<extensions />` clause as described here.

Since NLog 4.0 assemblies with the name "NLog*.dll", like “NLog.CustomTarget.dll” are now loaded automatically. This assembly should be in the same folder as `NLog.dll`. 

Configuration file example:
```xml
<nlog> 
  <extensions> 
    <add assembly="MyAssembly"/> 
  </extensions> 
  <targets> 
    <target name="a1" type="MyFirst" host="localhost"/> 
  </targets> 
  <rules> 
    <logger name="*" minLevel="Info" appendTo="a1"/> 
  </rules> 
</nlog>
```
##How to pass configuration options to the target?
Consider the above example. There’s a property called “Host” that does just that. Having a public property that sets the required configuration parameters is enough for NLog to use it. Each attribute that you put in the `<target />` definition gets passed to the appropriate public property. NLog takes care of the appropriate conversions necessary so that you can use integer, string, datetime, boolean parameters.

##Do I really need to create a separate DLL?
Not really. You can use `TargetFactory.AddTarget()` to register your target programmatically. Just be sure to do it at the very beginning of your program before any log messages are written. It should be possible to reference your EXE using the `<extensions />` clause.
```csharp
static void Main(string[] args) 
{ 
    ConfigurationItemFactory.Default.Targets
                            .RegisterDefinition("MyFirst", typeof(MyNamespace.MyFirstTarget));
 
    // start logging here 
}
```