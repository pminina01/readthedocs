Matches when the calculated layout is NOT equal to the specified substring. This filter is deprecated in favour of \<when /> which is based on contitions. 

Supported in .NET, Silverlight, Compact Framework and Mono.
## Configuration Syntax
```
<rules>
  <logger ... >
    <filters>
      <whenNotEqual ignoreCase="Boolean" layout="Layout" action="Enum" compareTo="String"/>
    </filters>
  </logger>
</rules>
```
## Parameters
### Filtering Options
* **layout** - Layout to be used to filter log messages. Layout Required.
* **action** - Action to be taken when filter matches. Required.  
Possible values:
  * _Ignore_ - The message should not be logged.
  * _IgnoreFinal_ - The message should not be logged and processing should be finished.
  * _Log_ - The message should be logged.
  * _LogFinal_ - The message should be logged and processing should be finished.
  * _Neutral_ - The filter doesn't want to decide whether to log or discard the message.
* **compareTo** - String to compare the layout to. Required.
* **ignoreCase** - Indicates whether to ignore case when comparing strings. Boolean Default: False