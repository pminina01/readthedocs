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
* `{message:when=logger=='logger'}`: print the message when the logger name is equal to "logger".
* `${when:inner=1:when='${aspnet-request:serverVariable=HTTPS}' == 'on'}${when:inner=0:when='${aspnet-request:serverVariable=HTTPS}' != 'on'}`: convert a layout string result to a bit (1 or 0) that can be inserted into a SQL bit field.

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


###Before 4.2.0

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

