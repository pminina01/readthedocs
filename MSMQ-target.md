Writes log message to the specified message queue handled by MSMQ. 

Supported in .NET, Compact Framework and Mono.
##Configuration Syntax
```xml
<targets>
  <target xsi:type="MSMQ"
          name="String"
          useXmlEncoding="Boolean"
          encoding="Encoding"
          layout="Layout"
          recoverable="Boolean"
          createQueueIfNotExists="Boolean"
          checkIfQueueExists="Boolean"
          label="Layout"
          queue="Layout" />
</targets>
```
Read more about using the [Configuration File](Configuration-file).
##Parameters
###General Options
_name_ - Name of the target.
###Layout Options
_useXmlEncoding_ - Indicates whether to use the XML format when serializing message. [Boolean](Data-types) Default: False

_encoding_ - Encoding to be used when writing text to the queue. [Encoding](Data-types)

_layout_ - Layout used to format log messages. [Layout](Data-types) Required. Default: ${longdate}|${level:uppercase=true}|${logger}|${message}
###Queue Options
_recoverable_ - Indicates whether to use recoverable messages (with guaranteed delivery). [Boolean](Data-types) Default: False

_createQueueIfNotExists_ - Indicates whether to create the queue if it doesn't exists. Won't do anything when _checkIfQueueExists_ is false.  [Boolean](Data-types) Default: False
_checkIfQueueExists_- If false, won't check for the existence of the queue. This is sometimes needed for private remote queues (where the `.exists` would throw an Exception). [Boolean](Data-types) Default: True

_label_ - Label to associate with each message. [Layout](Data-types) Default: NLog  
By default no label is associated.

_queue_ - Name of the queue to write to. [Layout](Data-types) Required.  
To write to a private queue on a local machine use .\private$\QueueName. For other available queue names, consult MSMQ documentation.

##Notes
The MSMQ target requires that:
* NLog.extended.dll be along side the NLog.dll at runtime.
* The machine doing the logging have MSMQ installed with the Active Directory Domain Services Integration option. If the option is not installed, the target will throw an exception.
* The queue being written to is NOT transactional.