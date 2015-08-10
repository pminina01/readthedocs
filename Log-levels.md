The following are the allowed log levels (in descending order):

* `Fatal`   
* `Error` 
* `Warn`  
* `Info`
* `Debug`
* `Trace`

Also to turn off logging, use `Off`

Examples when you could use which level:
|Level|Example|
------|-------
|Fatal|Highest level: important stuff down|
|Error|For example application crashes / exceptions.|
|Warn|Incorrect behavior but the application can continue |
|Info|Normal behavior like mail sent, user updated profile etc.|
|Debug|Executed queries, user authenticated, session expired|
|Trace|Begin method X, end method X etc|
