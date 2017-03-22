Writes log message to the specified message queue handled by MSMQ. 

Supported in .NET, Compact Framework and Mono.
## Configuration Syntax
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
Read more about using the [[Configuration File]].

## Parameters
### General Options
* **name** - Name of the target.
###Layout Options
* **useXmlEncoding** - Indicates whether to use the XML format when serializing message. [Boolean](Data-types) Default: False

* **encoding** - Encoding to be used when writing text to the queue. [Encoding](Data-types)

* **layout** - Layout used to format log messages. [Layout](Data-types) Required. Default: `${longdate}|${level:uppercase=true}|${logger}|${message}`

### Queue Options
* **queue** - Name of the queue to write to. [Layout](Data-types) **Required**.  
To write to a private queue on a local machine use .\private$\QueueName. For other available queue names, consult MSMQ documentation.

* **recoverable** - Indicates whether to use recoverable messages (with guaranteed delivery). [Boolean](Data-types) Default: False

* **createQueueIfNotExists** - Indicates whether to create the queue if it doesn't exists. Won't do anything when _checkIfQueueExists_ is false.  [Boolean](Data-types) Default: False

* **checkIfQueueExists** - If false, won't check for the existence of the queue. This is sometimes needed for private remote queues (where the `.exists` would throw an Exception). [Boolean](Data-types) Default: True

* **label** - Label to associate with each message. [Layout](Data-types) Default: "NLog"

## Notes
The MSMQ target requires that:
* NLog.extended.dll be along side the NLog.dll at runtime.
* The machine doing the logging have MSMQ installed with the Active Directory Domain Services Integration option. If the option is not installed, the target will throw an exception.
* The queue being written to is NOT transactional.