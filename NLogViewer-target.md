Sends log messages to the remote instance of NLog Viewer. 

Supported in .NET, Silverlight, Compact Framework and Mono.
## Configuration Syntax
```xml
<targets>
  <target xsi:type="NLogViewer"
          name="String"
          newLine="Boolean"
          layout="Layout"
          onOverflow="Enum"
          maxMessageSize="Integer"
          encoding="Encoding"
          connectionCacheSize="Integer"
          address="Layout"
          keepConnection="Boolean"
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
> This parameter is not supported in:
> * NLog v1.0 for .NET Compact Framework 1.0
> * NLog v1.0 for .NET Compact Framework 2.0
> * NLog v1.0 for .NET Framework 1.0
> * NLog v1.0 for .NET Framework 1.1
> * NLog v1.0 for .NET Framework 2.0

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
> This parameter is not supported in:
> * NLog v1.0 for .NET Compact Framework 1.0
> * NLog v1.0 for .NET Compact Framework 2.0
> * NLog v2.0 for .NET Compact Framework 2.0
> * NLog v2.0 for .NET Compact Framework 3.5
> * NLog v2.0 for Silverlight 2.0
> * NLog v2.0 for Silverlight 3.0
> * NLog v2.0 for Silverlight 4.0
> * NLog v2.0 for Silverlight for Windows Phone 7
> * NLog v2.0 for Silverlight for Windows Phone 7.1

* **includeCallSite** - Indicates whether to include call site (class and method name) in the information sent over the network. [Boolean](Data-types)  
> This parameter is not supported in:
> * NLog v1.0 for .NET Compact Framework 1.0
> * NLog v1.0 for .NET Compact Framework 2.0
> * NLog v2.0 for .NET Compact Framework 2.0
> * NLog v2.0 for .NET Compact Framework 3.5

* **appInfo** - AppInfo field. By default it's the friendly name of the current AppDomain.

* **ndcItemSeparator** - NDC item separator.
> This parameter is not supported in:
> * NLog v1.0 for .NET Compact Framework 1.0
> * NLog v1.0 for .NET Compact Framework 2.0
> * NLog v1.0 for .NET Framework 1.0
> * NLog v1.0 for .NET Framework 1.1
> * NLog v1.0 for .NET Framework 2.0

* **includeNdc** - Indicates whether to include NestedDiagnosticsContext stack contents. [Boolean](Data-types)

* **includeNLogData** - Indicates whether to include NLog-specific extensions to log4j schema. [Boolean](Data-types)

* **parameters** - The collection of parameters. Each parameter contains a mapping between NLog layout and a named parameter. [Collection](Data-types) 
Each collection item is represented by \<parameter /> element with the following attributes:

* **layout** - Layout that should be use to calcuate the value for the parameter. [Layout](Data-types) Required.

* **name** - Viewer parameter name. Required.
* **includeMdc** - Indicates whether to include MappedDiagnosticsContext dictionary contents. [Boolean](Data-types)