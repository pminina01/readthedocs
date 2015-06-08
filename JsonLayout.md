A specialized layout that renders to JSON.

```xml
<target name="jsonFile" xsi:type="File" fileName="${logFileNamePrefix}.json">
      <layout xsi:type="JsonLayout">
              <attribute name="time" layout="${longdate}" />
              <attribute name="level" layout="${level:upperCase=true}"/>
              <attribute name="message" layout="${message}" />
       </layout>
</target>
```

This would write: `{ "time": "2010-01-01 12:34:56.0000", "level": "ERROR", "message": "hello, world" }`

==Note
Currenlty only (non-nested) key-values are supported.