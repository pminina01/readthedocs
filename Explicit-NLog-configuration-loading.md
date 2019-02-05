# Loading NLog configuration from file
NLog will automatically [scan for configuration files](Configuration-file#configuration-file-locations), but sometimes the platform requires explicit configuration loading like this:

```c#
NLog.LogManager.Configuration = new NLog.Config.XmlLoggingConfiguration("nlog.config");
```

# Loading NLog configuration from string
The configuration can also come from standard string like this:

```c#
string currentDir = System.IO.Directory.GetCurrentDirectory();
System.IO.StringReader sr = new System.IO.StringReader(xmlString);
System.Xml.XmlReader xr = System.Xml.XmlReader.Create(sr);
NLog.LogManager.Configuration = new NLog.Config.XmlLoggingConfiguration(xr, currentDir);
```

# Loading NLog configuration from resource in Xamarin
You need to put the NLog.config file into the library project, then edit file's properties - change the **build action** to **embedded resource**.

```c#
public static Stream GetEmbeddedResourceStream(Assembly assembly, string resourceFileName)
{
  var resourcePaths = assembly.GetManifestResourceNames()
    .Where(x => x.EndsWith(resourceFileName, StringComparison.CurrentCultureIgnoreCase))
    .ToList();
  if (resourcePaths.Count == 1)
  {
    return assembly.GetManifestResourceStream(resourcePaths.Single());
  }
  return null;
}

var nlogConfigFile = GetEmbeddedResourceStream(myAssembly, "NLog.config");
if (nlogConfigFile != null)
{
    var xmlReader = XmlReader.Create(nlogConfigFile);
    LogManager.Configuration = new XmlLoggingConfiguration(xmlReader, res);
}
```