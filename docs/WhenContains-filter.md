Matches when the calculated layout contains the specified substring. This filter is deprecated in favour of \<when /> which is based on conditions. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
<rules>
  <logger ... >
    <filters>
      <whenContains layout="Layout" substring="String" action="Enum" ignoreCase="Boolean"/>
    </filters>
  </logger>
</rules>
```

## Parameters
### Filtering Options
* **layout** - Layout to be used to filter log messages. Layout Required.
* **substring** - Substring to be matched. Required.
* **action** - Action to be taken when filter matches. Required.  
Possible values:
  * _Ignore_ - The message should not be logged.
  * _IgnoreFinal_ - The message should not be logged and processing should be finished.
  * _Log_ - The message should be logged.
  * _LogFinal_ - The message should be logged and processing should be finished.
  * _Neutral_ - The filter doesn't want to decide whether to log or discard the message.
* **ignoreCase** - Indicates whether to ignore case when comparing strings. Boolean Default: False