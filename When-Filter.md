Filter events in the config.

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```xml
<rules>
  <logger ... >
    <filters>
      <when condition="Condition" action="Enum"/>
    </filters>
  </logger>
</rules>
```

## Parameters
### Filtering Options
* **condition** - Condition expression. Condition Required. See section Conditions below.
* **action** - Action to be taken when filter matches. Required.  
Possible values:
  * `Ignore` - The message should not be logged.
  * `IgnoreFinal` - The message should not be logged and processing should be finished.
  * `Log` - The message should be logged.
  * `LogFinal` - The message should be logged and processing should be finished.
  * `Neutral` - The filter doesn't want to decide whether to log or discard the message.


## Conditions 
Conditions are expressions used with the `<when>` filter. They consist of one or more tests. They are used in the filter to determine if an action will be taken.

### Condition Language
The filter expressions are written in a special mini-language. The language consists of:
* relational operators: `==`, `!=`, `<`, `<=`, `>=` and `>`
<br>_Note: Some [predefined XML characters](https://en.wikipedia.org/wiki/List_of_XML_and_HTML_character_entity_references#Predefined_entities_in_XML) may need to be escaped.  For example, if you try to use the '<' character, the XML parser will interpret it as an opening tag which results in an error in the configuration file.  Instead, use the escaped version of '<' (`&lt;`) in this context._
* boolean operators: `and`, `or`, `not`
* string literals which are always evaluated as layouts - `${somerenderer}`
* boolean literals - `true` and `false`
* numeric literals - e.g. `12345` (integer literal) and `12345.678` (floating point literal)
* log level literals - `LogLevel.Trace`, `LogLevel.Debug`, ... `LogLevel.Fatal`
* predefined keywords to access the most common log event properties - `level`, `message` and `logger`
* braces - to override default priorities and group expressions together
* condition functions - to perform `string` and `object` tests
* Single quotes should be escaped with another single quote. 

### Condition Functions
The following condition functions are available:
* `contains(s1,s2)` Determines whether the second string is a substring of the first one. Returns: `true` when the second string is a substring of the first string, `false` otherwise.
* `ends-with(s1,s2)` Determines whether the second string is a suffix of the first one. Returns: `true` when the second string is a prefix of the first string, `false` otherwise.
* `equals(o1,o2)` Compares two objects for equality. Returns: `true` when two objects are equal, `false` otherwise.
* `length(s)` Returns the length of a string.
* `starts-with(s1,s2)` Determines whether the second string is a prefix of the first one. Returns: `true` when the second string is a prefix of the first string, `false` otherwise.


### Quotes
Single quotes should be escaped with another single quote. 
Example:

```
contains('${message}', 'Cannot insert the value NULL into column ''Col1')
```

## Extensibility
New condition functions are easy to add; just create a public static class with a static function and mark the class and method with the attributes `[ConditionMethods]` and `[ConditionMethod]` respectively. 

You can find a sample implementation of a custom filter [here](https://github.com/NLog/NLog/blob/8201a362b8702be97facae2c6af83c2a6e9b54d1/tests/SampleExtensions/MyConditionMethods.cs)

Then you have to tell NLog where to find your assembly

```xml
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.netfx35.xsd" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" >
    <extensions>
		<add assembly="NLog.Extensions" />
    </extensions>
   ...
<nlog>
```

## Examples
Here are several examples with conditions:

```xml
<rules>
    <logger name="*" writeTo="file">
        <filters>
            <when condition="length('${message}') > 100" action="Ignore" />
            <when condition="equals('${logger}','MyApps.SomeClass')" action="Ignore" />
            <when condition="(level >= LogLevel.Debug and contains('${message}','PleaseDontLogThis')) or level==LogLevel.Warn" action="Ignore" />
            <when condition="not starts-with('${message}','PleaseLogThis')" action="Ignore" />
        </filters>
    </logger>
</rules>
```

Ignore all `Microsoft.*` logs but log `Microsoft.AspNetCore.Hosting.Internal.WebHost`. `Log` -> `Ignore` order is important.
```xml
<rules>
    <logger name="*" writeTo="file">
        <filters>
            <when condition="equals(logger, 'Microsoft.AspNetCore.Hosting.Internal.WebHost')" action="Log" />
            <when condition="starts-with(logger, 'Microsoft')" action="Ignore" />
        </filters>
    </logger>
</rules>
```