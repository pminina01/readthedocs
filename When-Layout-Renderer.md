Only outputs the inner layout when the specified condition has been met.  See [Conditions page](https://github.com/NLog/NLog/wiki/Conditions).

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${when:when=Condition:inner=Layout:else=Layout}
```

or by using ambient property to modify output of other layout renderer:

```
${other:when=Condition}
```

##Parameters
###Transformation Options
* _when_ - Condition that must be met for the inner layout to be printed. Condition Required.
* _inner_ - Wrapped layout. Layout
* _else_ - Layout if the condition is not true (introduced in NLog 4.3.5)

##Examples

print the message when the logger name is equal to "logger": 
 ```
${message:when=logger=='logger'}
```
 
convert a layout string result to a bit (1 or 0) that can be inserted into a SQL bit field.:

```
${when:when='${aspnet-request:serverVariable=HTTPS}' == 'on':inner=1:else:0}
```

Write "Good" if the loglevel is trace/debug/info and otherwise "Bad":

```
${when:when=level<=LogLevel.Info:inner=Good:else=Bad}
```

##Escaping

### Since 4.2 

When using `:` and `}` in a internal layout those characters need to be scape (there is no need to scape `\`).

-  `:` because it's a value separator. 
-  `}` because it's the end of the layout

Working examples:

- `${when:when=1 == 1:Inner=Test\: Hello}`
- `${when:when=1 == 1:Inner=Test\\Hello}`
- `${when:when=1 == 1:Inner=Test\Hello}`
- `${when:when=1 == 1:Inner=Test{Hello\}}`


###Before 4.2

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

