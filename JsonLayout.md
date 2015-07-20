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

Added in NLog 4.1

Optional _encode_ parameter.

You can disable JSON encoding by setting **encode="false"**. This will let you to write any string without JSON encoding. Including custom JSON.

```xml
<attribute name="Details" layout="${event-context:item=Details}" encode="false" />
```

##Parameters
* _name_: required. The name of the key in JSON
* _layout_: The (layout)[layout] for they key.
* _encode_: Enable or disable JSON encoding for the attribute. Enabled by default. (Added in NLog 4.1) 
* _suppressSpaces_: Enable to suppress extra spaces in the output JSON.  Disabled by default. (Added in NLog 4.1)

## Notes
* Currently the layout will always create an non-nested object with properties.
* The JSON will be written on one line, so no newlines. 
