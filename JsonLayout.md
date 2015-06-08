A specialized layout that renders to JSON.

Added in NLog 4.0


```xml
<target name="jsonFile" xsi:type="File" fileName="${logFileNamePrefix}.json">
      <layout xsi:type="JsonLayout">
              <attribute name="time" layout="${longdate}" />
              <attribute name="level" layout="${level:upperCase=true}"/>
              <attribute name="message" layout="${message}" />
       </layout>
</target>
```

This would write: 

```json
{ "time": "2010-01-01 12:34:56.0000", "level": "ERROR", "message": "hello, world" }
```

##Parameters

* _name_: required. The name of the key in JSON
* _layout_: The (layout)[layout] for they key.

## Notes
* Currently the layout will always create an non-nested object with properties.
* Also there is no way to prevent escaping of the values (e.g. writing custom JSON as value)
* The JSON will be written on one line, so no newlines. 