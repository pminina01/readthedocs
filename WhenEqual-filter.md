Matches when the calculated layout is equal to the specified substring. This filter is deprecated in favour of \<when /> which is based on contitions. 

Supported in .NET, Silverlight, Compact Framework and Mono
##Configuration Syntax
```
<rules>
  <logger ... >
    <filters>
      <whenEqual ignoreCase="Boolean" layout="Layout" action="Enum" compareTo="String"/>
    </filters>
  </logger>
</rules>
```
##Parameters
###Filtering Options
* _ignoreCase_ - Indicates whether to ignore case when comparing strings. Boolean Default: False
* _layout_ - Layout to be used to filter log messages. Layout Required.
* _action_ - Action to be taken when filter matches. Required.  
Possible values:  
  * Ignore - The message should not be logged.
  * IgnoreFinal - The message should not be logged and processing should be finished.
  * Log - The message should be logged.
  * LogFinal - The message should be logged and processing should be finished.
  * Neutral - The filter doesn't want to decide whether to log or discard the message.
* _compareTo_ - String to compare the layout to. Required.