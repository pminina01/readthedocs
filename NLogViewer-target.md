Sends log messages to the remote instance of NLog Viewer. For example, [Log4View](http://www.log4view.com/log4view/)

Supported in .NET, Silverlight, Compact Framework and Mono.
## Configuration Syntax
```xml
<targets>
  <target xsi:type="NLogViewer"
          name="String"
          layout="Layout"
          newLine="Boolean"
          onOverflow="Enum"
          maxMessageSize="Integer"
          encoding="Encoding"
          connectionCacheSize="Integer"
          address="Layout"
          keepConnection="Boolean"
          onConnectionOverflow="Enum"
          includeSourceInfo="Boolean"
          includeCallSite="Boolean"
          appInfo="String"
          ndcItemSeparator="String"
          includeNdc="Boolean"
          includeNLogData="Boolean"
          includeMdc="Boolean">
    <parameter layout="Layout" name="String"/><!-- repeated -->
  </target>
</targets>
```
Read more about using the [Configuration File](Configuration-file).

This target inherits from the [Network Target](Network-target), and so it has also all the properties of the Network Target available. 

## Parameters
### General Options
* **name** - Name of the target.

### Layout Options
* **newLine** - Indicates whether to append newline at the end of log message. [Boolean](Data-types) Default: False

* **layout** - Instance of Log4JXmlEventLayout that is used to format log messages. [Layout](Data-types) Default: ${longdate}|${level:uppercase=true}|${logger}|${message}

* **onOverflow** - Action that should be taken if the message is larger than maxMessageSize.  
Possible values:
  * _Discard_ - Discard the entire message.
  * _Error_ - Report an error.
  * _Split_ - Split the message into smaller pieces.

* **maxMessageSize** - Maximum message size in bytes. [Integer](Data-types) Default: 65000

* **encoding** - Encoding to be used. [Encoding](Data-types) Default: utf-8

### Connection Options
* **connectionCacheSize** - Size of the connection cache (number of connections which are kept alive). [Integer](Data-types) Default: 5

* **address** - Network address. [Layout](Data-types)  
The network address can be:
  * tcp://host:port - TCP (auto select IPv4/IPv6) (not supported on Windows Phone 7.0)
  * tcp4://host:port - force TCP/IPv4 (not supported on Windows Phone 7.0)
  * tcp6://host:port - force TCP/IPv6 (not supported on Windows Phone 7.0)
  * udp://host:port - UDP (auto select IPv4/IPv6, not supported on Silverlight and on Windows Phone 7.0)
  * udp4://host:port - force UDP/IPv4 (not supported on Silverlight and on Windows Phone 7.0)
  * udp6://host:port - force UDP/IPv6 (not supported on Silverlight and on Windows Phone 7.0)
  * http://host:port/pageName - HTTP using POST verb
  * https://host:port/pageName - HTTPS using POST verb
  For SOAP-based webservice support over HTTP use WebService target.

* **keepConnection** - Indicates whether to keep connection open whenever possible. [Boolean](Data-types) Default: True

### Payload Options
* **includeSourceInfo** - Indicates whether to include source info (file name and line number) in the information sent over the network. [Boolean](Data-types)  


* **includeCallSite** - Indicates whether to include call site (class and method name) in the information sent over the network. [Boolean](Data-types)  

* **appInfo** - AppInfo field. By default it's the friendly name of the current AppDomain.

* **ndcItemSeparator** - NDC item separator.

* **includeNdc** - Indicates whether to include NestedDiagnosticsContext stack contents. [Boolean](Data-types)

* **includeNLogData** - Indicates whether to include NLog-specific extensions to log4j schema. [Boolean](Data-types)

* **includeMdc** - Indicates whether to include MappedDiagnosticsContext dictionary contents. [Boolean](Data-types)

* **parameters** - The collection of parameters. Each parameter contains a mapping between NLog layout and a named parameter. [Collection](Data-types) 
Each collection item is represented by `<parameter />` element with the following attributes:

  * **layout** - Layout that should be use to calcuate the value for the parameter. [Layout](Data-types) Required.

  * **name** - Viewer parameter name. Required.


## Example

```xml
<?xml version="1.0" encoding="utf-8"?>

<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://www.nlog-project.org/schemas/NLog.xsd NLog.xsd"
      autoReload="true"
      throwExceptions="true"
      internalLogLevel="Warn" internalLogFile="c:\temp\nlog-internal.log">

  <targets>


    <target name="log4view" xsi:type="NLogViewer" address="tcp://127.0.0.1:878" 
                 KeepConnection="false" OnConnectionOverflow="Block" MaxConnections="5" />
  
    <target xsi:type="ColoredConsole" name="console" layout="${longdate} ${logger} ${uppercase:${level}} ${message}" />
  </targets>

  <rules>
    <logger name="*" minlevel="Trace" writeTo="log4view" />
  </rules>
</nlog>
```

note: ignore the XSD errors.