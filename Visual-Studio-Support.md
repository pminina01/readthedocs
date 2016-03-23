NLog integrates with Visual Studio® 2005/2008 and 2010 (including Visual C# and Visual Basic.NET Express Editions). Integration with Visual Studio.NET 2002 and 2003 is also supported, but not all features are available.

##Intellisense(TM)
NLog supports Intellisense when editing XML configuration files (both App.config-style, and stand-alone). All you need to do is add two namespace declarations to the `\<nlog>` tag:
```
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd" 
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
  <!-- configuration goes here --> 
</nlog>
```

The other change necessary is turning  
`<target type=“TypeName”/>`  
to  
`<target xsi:type=“TypeName”/>`.

Once you do this, you really good support for Intellisense and config file validation in Visual Studio.


##Integration with Add/Reference dialog
NLog Setup registers the appropriate AssemblyFolders entry in registry so that Visual Studio is able to locate the *.dll files and present them in Add Reference dialog. This is supported in all Visual Studio versions.


##New Item Templates
NLog comes with 3 sample configuration files that can be quickly added to you project through Add New Item dialog. They are:
* configuration file that defines one File Target (typical)
* configuration file that defines one Console Target
* empty configuration file

Please note that you need to change “Copy To Output Directory” option on the NLog.config to “Copy Always”


Note that “New Item” templates are supported on Visual Studio 2005 and higher (including Express Editions).

##Code Snippets
NLog installs a Visual Studio 2005 Code Snippet called “nlogger” that can be used to quickly declare a logger instance. It inserts the following piece of text:
```csharp
private static Logger logger = LogManager.GetCurrentClassLogger();
```