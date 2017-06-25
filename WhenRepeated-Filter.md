Matches when the calculated layout has already been logged. Useful if having an aggressive logger, and wants to throttle the output.

Introduced with NLog ver. 4.5

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
<rules>
  <logger ... >
    <filters>
      <whenRepeated layout="Layout" timeoutSeconds="30" action="Enum" />
    </filters>
  </logger>
</rules>
```

## Parameters
### Filtering Options
* **layout** - Layout to be used to filter log messages. Layout Required.
* **timeoutSeconds** - How long to ignore identical messages before logging again (Default 10 secs)
* **action** - Action to be taken when filter matches. Required.  
Possible values:
  * _Ignore_ - The message should not be logged.
  * _IgnoreFinal_ - The message should not be logged and processing should be finished.
  * _Log_ - The message should be logged.
  * _LogFinal_ - The message should be logged and processing should be finished.
  * _Neutral_ - The filter doesn't want to decide whether to log or discard the message.
### Logging Options
* **FilterCountPropertyName** - Tell how many identical log messages has been ignored. By adding LogEvent-Property with this name to the next LogEvent after timeout expires.
* **FilterCountMessageAppendFormat** - Tell how many identical log messages has been ignored. By appending to LogEVent-Message to the next LogEvent after timeout expires (Ex. " (Hits: {0}")

## Advanced Parameters
* **MaxLength** - Max number of characters to include when checking for identical messages (Default 1000 characters)
* **MaxFilterCacheSize** - Max number of unique log messages to keep in cache, before starting to prune (Default 50000)
* **DefaultFilterCacheSize** - Initial start size of the cache for keep track of unique log messages (Default 1000)