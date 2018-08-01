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