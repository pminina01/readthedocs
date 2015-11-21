Sends log messages over the network. 


For SOAP-based webservice support over HTTP use [WebService target](https://github.com/NLog/NLog/wiki/WebService-target).

Supported in .NET, Silverlight, Compact Framework and Mono.
##Configuration Syntax
```xml
<targets>
  <target xsi:type="Network"
          name="String"
          onOverflow="Enum"
          newLine="Boolean"
          layout="Layout"
          maxMessageSize="Integer"
          encoding="Encoding"
          
          connectionCacheSize="Integer"
          maxConnections="Integer"
          maxQueueSize="Integer"
          keepConnection="Boolean"
          onConnectionOverflow="Enum"
          address="Layout" 
/>
</targets>
```
Read more about using the [Configuration File](Configuration-file).
##Parameters
###General Options
_name_ - Name of the target.
###Layout Options
_onOverflow_ - Action that should be taken if the message is larger than maxMessageSize.  
Possible values:
* Discard - Discard the entire message.
* Error - Report an error.
* Split - Split the message into smaller pieces.

_newLine_ - Indicates whether to append newline at the end of log message. [Boolean](Data-types) Default: False

_layout_ - Layout used to format log messages. [Layout](Data-types) Required. Default: `${longdate}|${level:uppercase=true}|${logger}|${message}`

_maxMessageSize_ - Maximum message size in bytes. [Integer](Data-types) Default: 65000

_encoding_ - Encoding to be used. [Encoding](Data-types) Default: utf-8
###Connection Options
_connectionCacheSize_ - Size of the connection cache (number of connections which are kept alive). [Integer](Data-types) Default: 5  


_keepConnection_ - Indicates whether to keep connection open whenever possible. [Boolean](Data-types) Default: True

_maxConnections_ - Maximum current connections. 0 = no maximum. `Integer` Default: `0`. Not used if _keepConnection_ is `true`

_onConnectionOverflow _- Action that should be taken if the will be more connections than _MaxConnections_.
Possible values:
* AllowNewConnnection - Just allow it. (default)
* Block - Block until there's more room in the queue.
* DiscardMessage - Discard the connection item.

_maxQueueSize_ - Maximum queue size. Only used for TCP (not http/https/udp). Will removes messages when if too many. 0 is no max. `Integer`. Default: 0

_address_ - Network address. [Layout](Data-types)  
The network address can be:
* tcp://host:port - TCP (auto select IPv4/IPv6) (not supported on Windows Phone 7.0)
* tcp4://host:port - force TCP/IPv4 (not supported on Windows Phone 7.0)
* tcp6://host:port - force TCP/IPv6 (not supported on Windows Phone 7.0)
* udp://host:port - UDP (auto select IPv4/IPv6, not supported on Silverlight and on Windows Phone 7.0)
* udp4://host:port - force UDP/IPv4 (not supported on Silverlight and on Windows Phone 7.0)
* udp6://host:port - force UDP/IPv6 (not supported on Silverlight and on Windows Phone 7.0)
* http://host:port/pageName - HTTP using POST verb
* https://host:port/pageName - HTTPS using POST verb

