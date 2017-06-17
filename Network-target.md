Sends log messages over the network. 


For SOAP-based webservice support over HTTP use [WebService target](https://github.com/NLog/NLog/wiki/WebService-target).

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```xml
<targets>
  <target xsi:type="Network"
          name="String"
          onOverflow="Enum"
          newLine="Boolean"
          lineEnding="CRLF|LF|CR|None"
          layout="Layout"
          maxMessageSize="Integer"
          encoding="Encoding"
          connectionCacheSize="Integer"
          maxConnections="Integer"
          maxQueueSize="Integer"
          keepConnection="Boolean"
          onConnectionOverflow="Enum"
          address="Layout" 
          includeSourceInfo="Boolean"
          includeCallSite="Boolean"
          appInfo="String"
          ndcItemSeparator="String"
          includeNdc="Boolean"
          includeNLogData="Boolean"
          includeMdc="Boolean"
/>
</targets>
```
Read more about using the [[Configuration File]].

## Parameters
### General Options
* **name** - Name of the target.

### Layout Options
* **onOverflow** - Action that should be taken if the message is larger than maxMessageSize.  
Possible values:
  * _Discard_ - Discard the entire message.
  * _Error_ - Report an error.
  * _Split_ - Split the message into smaller pieces.

* **newLine** - Indicates whether to append newline at the end of log message. [Boolean](Data-types) Default: False

* **layout** - Layout used to format log messages. [Layout](Data-types) Required. Default: `${longdate}|${level:uppercase=true}|${logger}|${message}`

* **maxMessageSize** - Maximum message size in bytes. [Integer](Data-types) Default: 65000

* **encoding** - Encoding to be used. [Encoding](Data-types) Default: utf-8

* **lineEnding** - Line Ending to be used if _newLine_ is set to true. `LineEndingMode` Default: `CRLF`. Not used if _newLine_ is `false`. Introduced in 4.3.8.
Possible values:
  * _CRLF_ - Carriage Return and Line Feed. (default)
  * _CR_ - Carriage Return.
  * _LF_ - Line Feed.
  * _None_ - No end of line characters.

### Connection Options
* **connectionCacheSize** - Size of the connection cache (number of connections which are kept alive). [Integer](Data-types) Default: 5  

* **keepConnection** - Indicates whether to keep connection open whenever possible. Not used for stateless protocols (= http, https) [Boolean](Data-types) Default: `True`

* **maxConnections** - Maximum current connections. 0 = no maximum. `Integer` Default: `0`. Not used if _keepConnection_ is `true`. Introduced in NLog 4.2.1

* **onConnectionOverflow** - Action that should be taken if the will be more connections than _maxConnections_ . Introduced in NLog 4.2.1. 
Possible values:
  * _AllowNewConnnection_ - Just allow it. (default)
  * _Block_ - Block until there's more room in the queue.
  * _DiscardMessage_ - Discard the connection item.

* **maxQueueSize** - Maximum queue size. Only used for TCP (not http/https/udp). Will removes messages when if too many. 0 is no max. `Integer`. Default: 0

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

### Payload Options
* **includeSourceInfo** - Indicates whether to include source info (file name and line number) in the information sent over the network. [Boolean](Data-types)  


* **includeCallSite** - Indicates whether to include call site (class and method name) in the information sent over the network. [Boolean](Data-types)  

* **appInfo** - AppInfo field. By default it's the friendly name of the current AppDomain.

* **ndcItemSeparator** - NDC item separator.

* **includeNdc** - Indicates whether to include NestedDiagnosticsContext stack contents. [Boolean](Data-types)

* **includeNLogData** - Indicates whether to include NLog-specific extensions to log4j schema. [Boolean](Data-types)

* **includeMdc** - Indicates whether to include MappedDiagnosticsContext dictionary contents. [Boolean](Data-types)
