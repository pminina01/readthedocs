The default approach for managing Loggers via LogManager class in NLog works well for homogenous applications where the main application and all the extension components are configured via a single configuration file. But sometimes you want to create a separate logging configuration, just for a particular component, plugin or extension.

In this case instead of using LogManager (which is global to an application), we need to use LogFactory object, which will be local to your component. LogFactory is for most practical purposes similar to LogManager, except that you can have multiple instances of this class in your application and each instance manages its own logging configuration (typically loaded from XML file).

When creating LogFactory you need to explicitly pass the configuration (either from a file or by programmatically constructing targets and rules) as in the following example:
```csharp
internal class MyLogManager 
{ 
    // A Logger dispenser for the current assembly (Remember to call Flush on application exit)
    public static LogFactory Instance { get { return _instance.Value; } }
    private static Lazy<LogFactory> _instance = new Lazy<LogFactory>(BuildLogFactory);

    // 
    // Use a config file located next to our current assembly dll 
    // eg, if the running assembly is c:\path\to\MyComponent.dll 
    // the config filepath will be c:\path\to\MyComponent.nlog 
    // 
    // WARNING: This will not be appropriate for assemblies in the GAC 
    // 
    private static LogFactory BuildLogFactory()
    {
         // Use name of current assembly to construct NLog config filename 
         Assembly thisAssembly = Assembly.GetExecutingAssembly(); 
         string configFilePath = Path.ChangeExtension(thisAssembly.Location, ".nlog"); 

         LogFactory logFactory = new LogFactory();
         logFactory.Configuration = new XmlLoggingConfiguration(configFilePath, true, logFactory); 
         return logFactory;
    }
}
```
Then all you need to do is to create loggers with:

`Logger logger = MyLogManager.Instance.GetLogger("name");`

or

`Logger logger = MyLogManager.Instance.GetCurrentClassLogger();`

If you want multiple assemblies to share this MyLogManager – just make it a public class and get others to use it.

You need to make sure that the configuration is properly closed when the process terminates (set MyLogManager.Instance.Configuration to null) or you may lose some log output. You may want to hook AppDomain.ProcessExit and AppDomain.DomainUnload events to turn off logging automatically. See the code of LogManager.cs for details.
