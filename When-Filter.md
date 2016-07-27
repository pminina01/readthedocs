Matches when the specified condition is met. 

Supported in .NET, Silverlight, Compact Framework and Mono.
##Configuration Syntax
```xml
<rules>
  <logger ... >
    <filters>
      <when condition="Condition" action="Enum"/>
    </filters>
  </logger>
</rules>
```
##Parameters
###Filtering Options
* _condition_ - Condition expression. Condition Required. See [Conditions page](https://github.com/NLog/NLog/wiki/Conditions).
* _action_ - Action to be taken when filter matches. Required.  
Possible values:
  * `Ignore` - The message should not be logged.
  * `IgnoreFinal` - The message should not be logged and processing should be finished.
  * `Log` - The message should be logged.
  * `LogFinal` - The message should be logged and processing should be finished.
  * `Neutral` - The filter doesn't want to decide whether to log or discard the message.

##Examples
See https://github.com/NLog/NLog/wiki/Conditions#examples

##Remarks
Conditions are expressed using a simple language described [here](Conditions).

