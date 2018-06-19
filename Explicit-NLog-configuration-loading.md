# Loading NLog configuration from file
NLog will automatically [scan for configuration files](Configuration-file#configuration-file-locations), but sometimes the platform requires explicit configuration loading like this:

```c#
NLog.LogManager.Configuration = new NLog.Config.XmlLoggingConfiguration("nlog.config");
```

# Loading NLog configuration from string
The configuration can also come from standard string like this:

```c#
System.Xml.XmlDocument xmlDoc = new System.Xml.XmlDocument();
xmlDoc.LoadXml(configXml);
string currentDir = System.IO.Directory.GetCurrentDirectory();
NLog.LogManager.Configuration = new NLog.Config.XmlLoggingConfiguration(xmlDoc.DocumentElement, currentDir);
```