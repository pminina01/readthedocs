The following article has related news post: [Extending NLog is... easy!](http://nlog-project.org/2015/06/30/extending-nlog-is-easy.html)

There could be various reasons why you would like to extend NLog. For example: If you want to write your log messages to a non-standard output or when you need a protocol which is not supported by NLog, you need to write a custom Target. If you use your own `${}` macro's, then a custom layout renderer is a good idea.  

This tutorial describes creating custom targets and custom layout renderers. But it's also possible to create custom Layouts and custom conditions (for filtering) - see [over here](https://github.com/NLog/NLog/wiki/Conditions#extensibility). 

##How to write a custom target?
See [How to write a custom target](How to write a custom target)

##How to use the custom target / layout renderer
It’s easy. Just put the target or layout renderer in a DLL and reference it from the the config file using the `<extensions />` clause as described here.

Starting from NLog 4.0 assemblies with the name "NLog*.dll", like “NLog.CustomTarget.dll” are now loaded automatically. This assembly should be in the same folder as `NLog.dll`. 

Configuration file example:
```xml
<nlog> 
  <extensions> 
    <add assembly="MyAssembly"/> 
  </extensions> 
  <targets> 
    <target name="a1" type="MyFirst" host="localhost"/> 
    <target name="f1" type="file"  layout="${longdate} ${hello-world}" 
            fileName="${basedir}/logs/logfile.log" />
  </targets> 
  <rules> 
    <logger name="*" minLevel="Info" appendTo="a1"/> 
    <logger name="*" minLevel="Info" appendTo="f1"/> 
  </rules> 
</nlog>
```


###Do I really need to create a separate DLL?
Not really. You can register your target programmatically. Just be sure to do it at the very beginning of your program before any log messages are written. It should be possible to reference your EXE using the `<extensions />` clause.
```csharp
static void Main(string[] args) 
{ 
    //target
    ConfigurationItemFactory.Default.Targets
                            .RegisterDefinition("MyFirst", typeof(MyNamespace.MyFirstTarget));

    //layout renderer
    ConfigurationItemFactory.Default.LayoutRenderers
                            .RegisterDefinition("hello-world", typeof(MyNamespace.HelloWorldLayoutRenderer ));
 
    // start logging here 
}
```