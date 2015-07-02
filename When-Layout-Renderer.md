Only outputs the inner layout when the specified condition has been met.  See [Conditions page](https://github.com/NLog/NLog/wiki/Conditions).

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${when:when=Condition:inner=Layout}
```

or by using ambient property to modify output of other layout renderer:

```
${other:when=Condition}
```

##Parameters
###Transformation Options
* _when_ - Condition that must be met for the inner layout to be printed. Condition Required.
* _inner_ - Wrapped layout. Layout


##Examples
* `{message:when=logger=='logger'}`: print the message when the logger name is equal to "logger"


##Remarks
The colon (:) character should be wrapped within ```{literal:text=\:}``` instead of placed directly within the _inner_ layout. 


**Working Example**
 
Configuration | `layout="${when:when=1 == 1:inner=Test${literal:text=\:} Hello${literal:text=\:} World}"`
------------- | -----------------------------------------------------------------------------------------
Output | `Test: Hello: World`


**Non-working Example**

Configuration | `layout="${when:when=1 == 1:inner=Test: Hello: World}"`
------------- | -------------------------------------------------------
Output | `World`

When the colon character is not wrapped only the last literal instance, in this case the word 'World', appears. 

:star: Workaround identified by: _@reedyrm_