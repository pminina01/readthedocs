Discards log messages. Used mainly for debugging and benchmarking. 

Supported in .NET, Silverligt, Compact Framework and Mono.
##Configuration Syntax
```xml
<targets>
  <target xsi:type="Null" name="String" formatMessage="Boolean" layout="Layout" />
</targets>
```
Read more about using the [Configuration File](Configuration-file).
##Parameters
###General Options
_name_ - Name of the target.
###Layout Options
_formatMessage_ - Indicates whether to perform layout calculation. [Boolean](Data-types) Default: False

_layout_ - Layout used to format log messages. [Boolean](Data-types) Required. Default: ${longdate}|${level:uppercase=true}|${logger}|${message}


##Example

```xml
<targets>
  <target xsi:type="Null" name="BlackHole" formatMessage="false"  />
</targets>
<rules>
   <!-- ignore events written that are written to a logger which starts with "Namespace." -->
   <logger name="Namespace.*" minlevel="Debug" writeTo="BlackHole" final="true" />     
</rules>
```