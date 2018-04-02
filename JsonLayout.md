A specialized layout that renders to JSON.

Added in NLog 4.0


```xml
<target name="jsonFile" xsi:type="File" fileName="${logFileNamePrefix}.json" >
      <layout xsi:type="JsonLayout" includeAllProperties="Boolean" excludeProperties="Comma-separated list (string)">
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

You can disable JSON encoding by setting **encode="false"**. This will let you to write any string without JSON encoding. Including custom JSON (Ex. boolean/numeric values)

```xml
<attribute name="Details" layout="${event-context:item=Details}" encode="false" />
```

## Parameters
* **Attribute**
  * **name** - Required. The name of the key in JSON
  * **layout** - The [layout](Layouts) for the key.
  * **encode** - Enable or disable JSON encoding for the attribute. Enabled by default.
  > Introduced in NLog 4.1
  * **escapeUnicode** - Escape unicode-characters (non-ascii) using **\u**. Enabled by default.
  > Introduced in NLog 4.4.7
* **suppressSpaces** - Enable to suppress extra spaces in the output JSON. Disabled by default.
  > Introduced in NLog 4.1
* **renderEmptyObject** - Gets or sets the option to render the empty object value `{}`, default `true`.
  > Introduced in NLog 4.3.7
* **includeMdc** - Indicates whether to include contents of the [[MappedDiagnosticsContext|MDC-Layout-Renderer]] dictionary. Boolean
  > Introduced in NLog 4.4.10
* **includeMdlc** - Indicates whether to include contents of the async [[MappedDiagnosticsLogicalContext|MDLC-Layout-Renderer]] dictionary. Boolean
  > Introduced in NLog 4.4.10 (.NET 4.0 or 4.5 required)
* **includeAllProperties** - Include all events properties of a logevent? default: `false`.
  > Introduced in NLog 4.4
* **excludeProperties** - comma separated string with names which properties to exclude. Only used when _includeAllProperties_ is `true`. Case sensitive. Default empty
When a name contains a comma, single quote the value. E.g. `'value,withquote',value2`.
  > Introduced in NLog 4.4
* **EscapeUnicode** - escape non-ascii characters? Boolean. Default `true`.
  > Introduced in NLog 4.4.7
* **MaxRecursionLimit** - How far should the JSON serializer follow object references before backing off. Integer. Default `0` (0 = No object reflection)
  > Introduced in NLog 4.5
 
## Notes
* Currently the layout will always create a non-nested object with properties.
* The JSON will be written on one line, so no newlines. 


## Advanced examples

Nested JSON layouts:

### From the API:

```c#
var jsonLayout = new JsonLayout
{
    Attributes =
    {
        new JsonAttribute("type", "${exception:format=Type}"),
        new JsonAttribute("message", "${exception:format=Message}"),
        new JsonAttribute("innerException", new JsonLayout
        {

            Attributes =
            {
                new JsonAttribute("type", "${exception:format=:innerFormat=Type:MaxInnerExceptionLevel=1:InnerExceptionSeparator=}"),
                new JsonAttribute("message", "${exception:format=:innerFormat=Message:MaxInnerExceptionLevel=1:InnerExceptionSeparator=}"),
            }
        },
        //don't escape layout
        false)
    }
};
```
returns: `{ "type": "NLog.NLogRuntimeException", "message": "test", "innerException": { "type": "System.NullReferenceException", "message": "null is bad!" } }`


### From XML

```xml
<nlog>
  <targets>
    <target name='jsonFile' type='File' fileName='log.json'>
      <layout type='JsonLayout'>
        <attribute name='time' layout='${longdate}' />
        <attribute name='level' layout='${level:upperCase=true}'/>
        <attribute name='nested' encode='false'  >
          <layout type='JsonLayout'>
            <attribute name='message' layout='${message}' />
            <attribute name='exception' layout='${exception}' />
          </layout>
        </attribute>
      </layout>
    </target>
  </targets>
  <rules>
      <logger name="*" minlevel="Debug" writeTo="jsonFile" />
  </rules>
</nlog>
```

will render: `{ "time": "2016-10-30 13:30:55.0000", "level": "INFO", "nested": { "message": "this is message", "exception": "test" } }`

## RenderEmptyObject 

```c#
var jsonLayout = new JsonLayout
{
    Attributes =
    {
        new JsonAttribute("type", "${exception:format=Type}"),
        new JsonAttribute("message", "${exception:format=Message}"),
        new JsonAttribute("innerException", new JsonLayout
        {

            Attributes =
            {
                new JsonAttribute("type", "${exception:format=:innerFormat=Type:MaxInnerExceptionLevel=1:InnerExceptionSeparator=}"),
                new JsonAttribute("message", "${exception:format=:innerFormat=Message:MaxInnerExceptionLevel=1:InnerExceptionSeparator=}"),
            },
            RenderEmptyObject = false
        },
        //don't escape layout
        false)
    }
   
};
```

Writing without an exception will render
`{ "type": "NLog.NLogRuntimeException", "message": "test" }`

with `RenderEmptyObject=true` (default) it will render:

` "type": "NLog.NLogRuntimeException", "message": "test", "innerException": {  } }`


## Nested JSON with structured logging

```c#
        public class TestObject
        {
            public string A { get; set; }
            public int B { get; set; }

            public override string ToString() { return A; }
        }
```

```c#
var testObj = new TestObject
{
    A = "AlphaObject",
    B = 2
};

var testObjB = new TestObject
{
    A = "BetaObject",
    B = 3
};

log.Info("First: {alpha}, Second: {beta}", testObj, testObjB)
```

With this config:

```xml
 <target xsi:type="File" name="jsonFile2" fileName="c:\temp\nlog-json-nested-${shortdate}.log">
     <layout type="JsonLayout">
         <attribute name="time" layout="${longdate}" />
         <attribute name="level" layout="${level}" />
         <attribute name="message" layout="${message}" />
         <attribute name="eventProperties" encode="false" >
             <layout type='JsonLayout' includeAllProperties="true"/>
         </attribute>
     </layout>
 </target>
```

Will render:

```json
{ "time": "2018-04-02 02:00:00.2349", "level": "Info", "message": "First: AlphaObject, Second: BetaObject", "eventProperties": { "alpha": {
  "A": "AlphaObject",
  "B": 2
}, "beta": {
  "A": "BetaObject",
  "B": 3
} } }

```

pretty printed:

```json
{
  "time": "2018-04-02 02:00:00.2349",
  "level": "Info",
  "message": "First: AlphaObject, Second: BetaObject",
  "eventProperties": {
    "alpha": {
      "A": "AlphaObject",
      "B": 2
    },
    "beta": {
      "A": "BetaObject",
      "B": 3
    }
  }
}
```

