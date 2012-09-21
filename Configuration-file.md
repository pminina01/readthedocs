##Configuration file locations
NLog attempts to automatically configure itself on startup, by looking for the configuration files in some standard places.

The following locations will be searched when executing a stand-alone *.exe application:
* standard application configuration file (usually applicationname.exe.config)
* applicationname.exe.nlog in application’s directory
* NLog.config in application’s directory
* NLog.dll.nlog in a directory where NLog.dll is located
* file name pointed by the NLOG_GLOBAL_CONFIG_FILE environment variable (if defined, NLog 1.0 only - support removed in NLog 2.0)

In case of an ASP.NET application, the following files are searched:
* standard web application file web.config
* web.nlog located in the same directory as web.config
* NLog.config in application’s directory
* NLog.dll.nlog in a directory where NLog.dll is located
* file name pointed by the NLOG_GLOBAL_CONFIG_FILE environment variable (if defined, NLog 1.0 only - support removed in NLog 2.0)

The .NET Compact Framework doesn’t recognize application configuration files (*.exe.config) nor environmental variables, so NLog only looks in these locations:
* applicationname.exe.nlog in application’s directory
* NLog.config in application’s directory
* NLog.dll.nlog in a directory where NLog.dll is located

##Configuration file format
NLog supports two configuration file formats:
 1. Configuration embedded within the standard *.exe.config or web.config file
 2. Simplified configuration, stored in a separate file

In the first variant, we use a standard configSections mechanism, which makes our file look like this:
```
<configuration>
  <configSections>
    <section name="nlog" type="NLog.Config.ConfigSectionHandler, NLog"/>
  </configSections>
  <nlog>
  </nlog>
</configuration>
```

The simplified format is the pure XML having the <nlog /> element as its root. The use of namespaces is optional, but it enables the Intellisense in Visual Studio.
```
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
</nlog>
```

Note that NLog config file is case-insensitive when not using namespaces and is case-sensitive when you use them. Intellisense only works with case-sensitive configurations.

Configuration elements You can use the following elements as children to <nlog />. The first two elements from the list are required to be present in all NLog configuration files, the remaining ones are optional and can be useful in advanced scenarios.
 * \<targets /> – defines log targets/outputs
 * \<rules /> – defines log routing rules
 * \<extensions /> – loads NLog extensions from the *.dll file
 * \<include /> – includes external configuration file
 * \<variable /> – sets the value of a configuration variable

##Targets
The \<targets /> section defines log [Targets](Targets). Each target is represented by a <target /> element. There are two attributes required for each target:
 * name – target name
 * type – target type – such as "File", "Database", "Mail". When using namespaces this attribute is named xsi:type.

In addition to these attributes, targets usually accept other parameters, which impact the way diagnostic traces are written. Each target has a different set of parameters, they are described in detail on project’s homepage and they are context-sensitive. Intellisense is also available in Visual Studio.

For example – the [File target](File Target) accepts the fileName parameter which defines output file name and the [Console target](Console Target) has the error parameter which determines whether the diagnostic traces are written to standard error (stderr) instead of standard output (stdout) of the process.

This example demonstrates a \<targets /> section which defines multiple targets: two files, one network target and OutputDebugString target:
```
<targets>
  <target name="f1" xsi:type="File" fileName="file1.txt"/>
  <target name="f2" xsi:type="File" fileName="file2.txt"/>  
  <target name="n1" xsi:type="Network" address="tcp://localhost:4001"/>
  <target name="ds" xsi:type="OutputDebugString"/>
</targets>
```