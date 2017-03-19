All configuration of NLog can be done with a single XML file. 

# Contents
[Configuration file locations](#configuration-file-locations)<br />
[Configuration file format](#configuration-file-format)<br />
[Log levels](#log-levels)<br />
[Targets](#targets)<br />
[Rules](#rules)<br />
[Example rules](#example-rules)<br />
[Layouts and layout renderers](#layouts-and-layout-renderers)<br />
[Include files](#include-files)<br />
[Variable](#variables)<br />
[Automatic reconfiguration](#automatic-reconfiguration)<br />
[Troubleshooting logging](#troubleshooting-logging)<br />
[Asynchronous processing and wrapper targets](#asynchronous-processing-and-wrapper-targets)<br />
[Default wrappers](#default-wrappers)<br />
[Default target parameters](#default-target-parameters)<br />
[Content escaping](#content-escaping)<br />
[Extensions](#extensions)

<a name="configuration-file-locations" />

## Configuration file locations
NLog attempts to automatically configure itself on startup, by looking for the configuration files in some standard places.

The following locations will be searched when executing a stand-alone *.exe application:
* standard application configuration file (usually applicationname.exe.config)
* applicationname.exe.nlog in application’s directory
* NLog.config in application’s directory
* NLog.dll.nlog in a directory where NLog.dll is located (only if NLog isn't installed in the GAC)

In case of an ASP.NET application, the following files are searched:
* standard web application file web.config
* web.nlog located in the same directory as web.config
* NLog.config in application’s directory
* NLog.dll.nlog in a directory where NLog.dll is located (only if NLog isn't installed in the GAC)

The .NET Compact Framework doesn’t recognize application configuration files (*.exe.config) nor environmental variables, so NLog only looks in these locations:
* applicationname.exe.nlog in application’s directory
* NLog.config in application’s directory
* NLog.dll.nlog in a directory where NLog.dll is located  (only if NLog isn't installed in the GAC)


### Xamarin Assets
For Xamarin Android, the assets folder is supported. "NLog.config" in the assets folder will be loaded automatically.
If the file name is different, then use:
```
LogManager.Configuration = new XmlLoggingConfiguration("assets/someothername.config");
````

<a name="configuration-file-format" />
## Configuration file format
NLog supports two configuration file formats:
 1. Configuration embedded within the standard *.exe.config or web.config file
 2. Simplified configuration, stored in a separate file

In the first variant, we use a standard configSections mechanism, which makes our file look like this:
```xml
<configuration>
  <configSections>
    <section name="nlog" type="NLog.Config.ConfigSectionHandler, NLog"/>
  </configSections>
  <nlog>
  </nlog>
</configuration>
```

The simplified format is the pure XML having the \<nlog /> element as its root. The use of namespaces is optional, but it enables the Intellisense in Visual Studio.
```xml
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
</nlog>
```

Note that NLog config file is case-insensitive when not using namespaces and is case-sensitive when you use them. Intellisense only works with case-sensitive configurations.

Configuration elements You can use the following elements as children to `<nlog />`. The first two elements from the list are required to be present in all NLog configuration files, the remaining ones are optional and can be useful in advanced scenarios.
 * `<targets />` – defines log targets/outputs
 * `<rules />` – defines log routing rules
 * `<extensions />` – loads NLog extensions from the *.dll file
 * `<include />`– includes external configuration file
 * `<variable />` – sets the value of a configuration variable

<a name="log-levels" />
## Log levels

The following are the allowed log levels (in descending order):

* `Fatal`   
* `Error` 
* `Warn`  
* `Info`
* `Debug`
* `Trace`

Also to turn off logging, use `Off`

Examples when you could use which level:

|Level|Example|
------|-------
|Fatal|Highest level: important stuff down|
|Error|For example application crashes / exceptions.|
|Warn|Incorrect behavior but the application can continue |
|Info|Normal behavior like mail sent, user updated profile etc.|
|Debug|Executed queries, user authenticated, session expired|
|Trace|Begin method X, end method X etc|


<a name="targets" />

## Targets
The \<targets /> section defines log [Targets](Targets). Each target is represented by a <target /> element. There are two attributes required for each target:
 * `name` – target name
 * `type` – target type – such as "File", "Database", "Mail". When using namespaces this attribute is named `xsi:type`.

In addition to these attributes, targets usually accept other parameters, which impact the way diagnostic traces are written. Each target has a different set of parameters, they are described in detail on project’s homepage and they are context-sensitive. Intellisense is also available in Visual Studio.

For example – the [File target](File Target) accepts the `fileName` parameter which defines output file name and the [Console target](Console Target) has the `error` parameter which determines whether the diagnostic traces are written to standard error (stderr) instead of standard output (stdout) of the process.

This example demonstrates a `<targets />` section which defines multiple targets: two files, one network target and OutputDebugString target:
```xml
<targets>
  <target name="f1" xsi:type="File" fileName="file1.txt"/>
  <target name="f2" xsi:type="File" fileName="file2.txt"/>  
  <target name="n1" xsi:type="Network" address="tcp://localhost:4001"/>
  <target name="ds" xsi:type="OutputDebugString"/>
</targets>
```

NLog provides many predefined [Targets](Targets). It’s actually very easy to create your own target - see [How to write a Target](How to write a Target).

<a name="rules" />

## Rules
Log routing rules are defined in the `<rules />` section. It is a simple routing table, where we define the list of targets that should be written to for each combination of source/logger name and [log level](/nlog/nlog/wiki/Log-levels). Rules are processed starting with the first rule in the list. When a rule matches, log messages are directed to target(s) in that rule. If a rule is marked as `final`, rules below it are not processed.

Each routing table entry is a \<logger /> element, which accepts the following attributes:
 * `name` – source/logger name (may include wildcard characters *)
 * `minlevel` – minimal log level for this rule to match
 * `maxlevel` – maximum log level for this rule to match
 * `level` – single log level for this rule to match
 * `levels` - comma separated list of log levels for this rule to match
 * `writeTo` – comma separated list of target that should be written to when this rule matches.
 * `final` – make this rule final. No further rules are processed when any final rule matches.
 * `enabled` - setting enabled to false allows to disable this rule. Disabled rules are ignored.

In case a rule, defined in a XML configuration, contains more than one level related keyword (`level`, `levels`, `minLevel` and `maxLevel`) only the first level declaring keyword or set is used and the rest are ignored.

The level related keywords are processed in the following order:

1. `level` 
2. `levels` 
3. `minlevel` and `maxlevel` (minimum and maximum level keywords have the same priority)
4. No keyword (All levels are logged)

In case a rule is marked as `final` and contains any level related keywords, the `final` attribute applies only to the specified levels.

<a name="example-rules" />

## Example rules
All messages from the `Class1` in the `Name.Space` whose level is `Debug` or higher are written to the "f1" target:
```xml
<logger name="Name.Space.Class1" minlevel="Debug" writeTo="f1" />
```

All messages from the `Class1` in the `Name.Space` whose level is either `Debug` or `Error` or higher are written to the "f1" target:
```xml
<logger name="Name.Space.Class1" levels="Debug,Error" writeTo="f1" />
```

Messages from any class in the `Name.Space` namespace are written to both "f3" and "f4" targets regardless of their levels:
```xml
<logger name="Name.Space.*" writeTo="f3,f4" />
```

Messages from any class in the `Name.Space` namespace whose level is between `Debug` and `Error` (which makes it `Debug`, `Info`, `Warn`, `Error`) are rejected (as there’s no `writeTo` clause) and no further rules are processed for them (because of the `final="true"` setting)
```xml
<logger name="Name.Space.*" minlevel="Debug" maxlevel="Error" final="true" />
```

In the simplest cases the entire logging configuration consists of a single `<target />` and a single `<logger />` rule that routes messages to this target depending on their level, but adding more targets and rules is very simple as the application grows.

<a name="layouts-and-layout-renderers" />

## Layouts and layout renderers
One of NLog’s strongest assets is the ability to use [layouts](Layouts). In the simplest form, layouts are texts with embedded tags delimited by `${` and `}`. The tags are called [Layout Renderers](Layout Renderers) and can be used to insert pieces of contextual information into the text.

Layouts can be used in many places, for example they can control the format of information written on the screen or sent to a file, but also to control the file names themselves. This is very powerful, which we’ll see in a moment.

Let’s assume, that we want to annotate each message written to the console with:
* current date and time
* name of the class and method that emitted the log message
* log level
* message text

This is very easy:
```xml
<target name="c" xsi:type="Console"  layout="${longdate} ${callsite} ${level} ${message}"/>
```

We can make each messages for each logger go to a separate file, as in the following example:
```xml
<target name="f" xsi:type="File" fileName="${logger}.txt"/>
```

As you can see, the ${logger} layout renderer was used in the fileName attribute, which causes each log message to be written to the file whose name includes the logger name. The above example will create the following files:
* Name.Space.Class1.txt
* Name.Space.Class2.txt
* Name.Space.Class3.txt
* Other.Name.Space.Class1.txt
* Other.Name.Space.Class2.txt
* Other.Name.Space.Class3.txt

<a name="include-files" />

## Include files
It’s sometimes desired to split the configuration file into many smaller ones. NLog provides an include file mechanism for that. To include an external file, you simply use `<include file=”…” />` element. It’s worth noting that the file attribute, just like most attributes in NLog config file(s), may include dynamic values using the familiar `${}` notation for layout renderers, so it’s possible to include different files based on environmental properties.

The following configuration example demonstrates this, by loading a file whose name is derived from the name of the machine we’re running on.
```xml
<nlog>
  ...
  <include file="${basedir}/${machinename}.config"/>
  ...
</nlog>
```

The optional attribute, `ignoreErrors="true"`, which defaults to `false`, can be added to prevent an exception from being thrown when the include file is not found or is not formatted correctly.  When setting `ignoreErrors="true"`, use the [Troubleshooting logging](#troubleshooting-logging) section to log errors.

Since NLog 4.4.2, wildcards (`*`) are allowed. E.g. `<include file="${basedir}/nlog-*.config"/>`

<a name="variables" />

## Variables
Variables can be used to write complex or repeated expressions (such as file names) in a concise manner. To define a variable use the following syntax:
```xml
<variable name="var" value="xxx" />
```

Once defined, variables can be used as if they were layout renderers – by using `${var}` syntax, as demonstrated in the following example:
```xml
<nlog>
  <variable name="logDirectory" value="${basedir}/logs/${shortdate}"/>
  <targets>
    <target name="file1" xsi:type="File" fileName="${logDirectory}/file1.txt"/>
    <target name="file2" xsi:type="File" fileName="${logDirectory}/file2.txt"/>
  </targets>
</nlog>
```

Variables should be declared before the targets to be able to use them. Otherwise configuration initialization will fail.

NB: Since NLog 4.3 the `${basedir}` isn't needed anymore for relative paths.

### Vars since NLog 4.1
In  NLog 4.1 is a new method introduced to render the variable values. Use `${var:var1}` instead of `${var1}`.

See [Variable layout renderer](https://github.com/NLog/NLog/wiki/Var-Layout-Renderer). 

Why use this new method? With the variable layout renderer:

* Variables can be changed, deleted and created from the API
* A default value can be configured for a variable, e.g. `${var:password:default=unknown}`

By default, variables are reset when the configuration reloads. In order to take the variables from current
configuration, add `keepVariablesOnReload="true"` parameter to the configuration file (introduced in NLog 4.4).
```xml
<nlog keepVariablesOnReload="true">
   ...
</nlog>
```



<a name="automatic-reconfiguration" />

## Automatic reconfiguration
The configuration file is read automatically at program startup. In a long running process (such as a Windows service or an ASP.NET application) it’s sometimes desirable to temporarily increase the log level without stopping the application. NLog can monitor logging configuration files and re-read them each time they are modified. To enable this mechanism, you simply add `autoReload="true"` parameter to the configuration file.
```xml
<nlog autoReload="true">
   ...
</nlog>
```

Note that automatic reconfiguration supports include files, so each time one of the included files is changed, the entire configuration gets reloaded.

_Just to make it explicit, automatic reloading will NOT stop/recycle the IIS Application Pool._

<a name="troubleshooting-logging" />
## Troubleshooting logging
Sometimes our application doesn’t write anything to the log files, even though we have supposedly configured logging properly. There can be many reasons for logs not being written. The most common problems are permissions issues, usually in an ASP.NET process, where the `aspnet_wp.exe` or `w3wp.exe` process may not have write access to the directory where we want to store logs.

NLog is designed to swallow run-time exceptions that may result from logging. The following settings can change this behavior and/or redirect these messages.
* `<nlog throwExceptions="true" />` - adding the `throwExceptions` attribute in the config file causes NLog to stop masking exceptions and pass them to the calling application instead. This attribute is useful at deployment time to quickly locate any problems. It’s recommended to set `throwExceptions` to `"false"` as soon as the application is properly configured to run, so that any accidental logging problems won’t crash the application. 
* `<nlog throwConfigExceptions="true" />`  - the same as `throwExceptions` but for configuration exceptions. If not set (or `null`), this is the same value as `throwExceptions`. Introduced in NLog 4.3. Default `null` (so same value as `throwExceptions`)
* `<nlog internalLogFile="file.txt" />` - adding `internalLogFile` causes NLog to write its internal debugging messages to the specified file. This includes any exceptions that may be thrown during logging.
* `<nlog internalLogLevel="Trace|Debug|Info|Warn|Error|Fatal" />` – determines the internal log level. The higher the level, the less verbose the internal log output.
* `<nlog internalLogToConsole="false|true" />` – determines whether internal logging messages are sent to the console.
* `<nlog internalLogToConsoleError="false|true" />` – determines whether internal logging messages are sent to the console error output (stderr).
* `<nlog internalLogToTrace="false|true" />` – determines whether internal logging messages are sent to the `System.Diagnostics.Trace`, which can be easily viewed in Visual Studio.

<a name="asynchronous-processing-and-wrapper-targets" />

## Asynchronous processing and wrapper targets
NLog provides wrapper and compound targets which modify other targets’ behavior by adding features like:
* asynchronous processing (wrapped target runs in a separate thread)
* retry-on-error
* load balancing
* buffering
* filtering
* failover (failover)

To define a wrapper in the configuration file, simply nest a target node within another target node. You can even wrap a wrapper target - there are no limits on depth. For example, to add asynchronous logging with retry-on-error functionality add this to your configuration file:
```xml
<targets>
  <target name="n" xsi:type="AsyncWrapper">
    <target xsi:type="RetryingWrapper">
      <target xsi:type="File" fileName="${file}.txt" />
    </target>
  </target>
</targets>
```

Because asynchronous processing is a common scenario, NLog supports a shorthand notation to enable it for all targets without the need to specify explicit wrappers. You can simply set `async="true"` on targets element and all your targets within that element will be wrapped with the `AsyncWrapper` target.
```xml
<nlog>
  <targets async="true">
    <!-- all targets in this section will automatically be asynchronous -->
  </targets>
</nlog>
```

<a name="default-wrappers" />

## Default wrappers
Sometimes we require ALL targets to be wrapped in the same way, for example to add buffering and/or retrying. NLog provides `<default-wrapper />` syntax for that. You simply put this element in the `<targets />` section and all your targets will be automatically wrapped with the specified wrapper. Note that `<default-wrapper />` applies to the single `<targets />` section only and you can have multiple sections so you can define groups of targets that are wrapped in a similar manner.
```xml
<nlog>  
  <targets>  
    <default-wrapper xsi:type="BufferingWrapper" bufferSize="100"/>  
    <target name="f1" xsi:type="File" fileName="f1.txt"/>  
    <target name="f2" xsi:type="File" fileName="f2.txt"/>  
  </targets>  
  <targets>  
    <default-wrapper xsi:type="AsyncWrapper">  
      <wrapper-target xsi:type="RetryingWrapper"/>  
    </default-wrapper>  
    <target name="n1" xsi:type="Network" address="tcp://localhost:4001"/>  
    <target name="n2" xsi:type="Network" address="tcp://localhost:4002"/>  
    <target name="n3" xsi:type="Network" address="tcp://localhost:4003"/>  
  </targets>  
</nlog>
```

In the above example we’ve defined two buffered File targets and three asynchronous and retrying Network targets.

<a name="default-target-parameters" />

## Default target parameters
Similar to default wrappers, NLog provides `<default-target-parameters />` which enables you to specify default values of target parameters. For example, if you don’t want files to be kept open, you can either add `keepFileOpen="false"` to each target, as in the following example:
```xml
<nlog>
  <targets>
    <target name="f1" xsi:type="File" fileName="f1.txt" keepFileOpen="false"/>
    <target name="f2" xsi:type="File" fileName="f2.txt" keepFileOpen="false"/>
    <target name="f3" xsi:type="File" fileName="f3.txt" keepFileOpen="false"/>
   </targets>
</nlog>
```

Alternatively you can specify a single `<default-target-parameters />` that applies to all targets in the `<targets />` section. Default parameters are defined on a per-type basis and are applied BEFORE the actual attributes defined in the XML file:
```xml
<nlog>
  <targets>
    <default-target-parameters xsi:type="File" keepFileOpen="false"/>
    <target name="f1" xsi:type="File" fileName="f1.txt"/>
    <target name="f2" xsi:type="File" fileName="f2.txt"/>
    <target name="f3" xsi:type="File" fileName="f3.txt"/>
  </targets>
</nlog>
```


<a name="content-escaping" />

## Content escaping
In the configuration file some characters needs to be escaped. 
Because it XML file, the `<` and `>` brackets should be escaped with `&lt;` and `&gt;`. This also holds for the attribute values, like a condition.

Inside a layout we need to escape the  `}` bracket and the colon `:` should be escaped because:

- `:` is the value separator.
- `}` is the end of the layout


Nested layout renderers doesn't need escaping. Also the backslash doesn't need an escape. 

Examples:

- `${appdomain:format={1\}{0\}}` (escape of `}`)
- `${rot13:inner=${ndc:topFrames=3:separator=x}}` (no escaping needed)
- `${when:when=1 == 1:Inner=Test\: Hello}` (escape of `:`)

<a name="extensions" />

## Extensions
Extensions can be configured to include additional NLog packages or custom ones:

Just reference the DLL in the config in the `<extensions />` as shown below.
The name should not include the `.dll`

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

Starting from NLog 4.0 assemblies with the name "NLog*.dll", like “NLog.CustomTarget.dll” are now loaded automatically. This assembly should be in the same folder as `NLog.dll`. 