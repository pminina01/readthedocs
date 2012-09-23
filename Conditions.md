Conditions are filter expressions used with the [when filter](whenFilter). They consist of one or more tests. They are used in the when filter to determine if an action will be taken.

##Language
The filter expressions are written in a special mini-language. The language consists of:
* relational operators: ==, !=, <, <=, >= and >
* boolean operators: and, or, not
* string literals which are always evaluated as layouts - '${somerenderer}'
* boolean literals - true and false
* numeric literals - 12345 (integer literal) and 12345.678 (floating point literal)
* log level literals - LogLevel.Trace, LogLevel.Debug, ... LogLevel.Fatal
* predefined keywords to access the most common log event properties - level, message and logger
* braces - to override default priorities and group expressions together
* condition functions - to perform string and object tests

##Functions
The following condition functions are available:
* contains(s1,s2) Determines whether the second string is a substring of the first one. Returns: true when the second string is a substring of the first string, false otherwise.
* ends-with(s1,s2) Determines whether the second string is a suffix of the first one. Returns: true when the second string is a prefix of the first string, false otherwise.
* equals(o1,o2) Compares two objects for equality. Returns: true when two objects are equal, false otherwise.
* length(s) Returns the length of a string.
* starts-with(s1,s2) Determines whether the second string is a prefix of the first one. Returns: true when the second string is a prefix of the first string, false otherwise.

##Examples
Here are several [when filter](whenFilter) examples with conditions:
```
<rules>
    <logger name="*" writeTo="file">
        <filters>
            <when condition="length(message) > 100" action="Ignore" />
            <when condition="equals('${logger}','MyApps.SomeClass')" action="Ignore" />
            <when condition="(level >= LogLevel.Debug and contains(message,'PleaseDontLogThis')) or level==LogLevel.Warn" action="Ignore" />
            <when condition="not starts-with('${message}','PleaseLogThis')" action="Ignore" />
        </filters>
    </logger>
</rules>
```

##Extensibility
New condition functions are easy to add; just create an ordinary function and mark it with the [ConditionMethod] attribute.