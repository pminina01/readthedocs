A layout that contains one or more nested layouts.

Introduced in NLog 4.3.6


```xml
<target name='file' type='File' fileName='log.txt'>
  <layout type='CompoundLayout'>
    <layout type='SimpleLayout' text="text1" />
    <layout type='SimpleLayout' text=" - " />
    <layout type='SimpleLayout' text="text2" />
  </layout>
</target>
```

```
text1 - text2
```

## Advanced examples

### From code

```c#
var compoundLayout = new CompoundLayout
{
    Layouts =
    {
        new SimpleLayout("myAmazingText: "),
        new JsonLayout
        {
            Attributes =
            {
                new JsonAttribute("time", "${longdate}"),
                new JsonAttribute("level", "${level:upperCase=true}"),
            }
        }
    }
};
```

```json
myAmazingText: { "time": "2016-10-30 13:30:55.0000", "level": "INFO" }
```

### From XML

```xml
<nlog>
  <targets>
    <target name='file' type='File' fileName='log.txt'>
      <layout type='CompoundLayout'>
        <layout type='SimpleLayout' text="myAmazingText: " />
        <layout type='JsonLayout'>
          <attribute name='time' layout='${longdate}' />
          <attribute name='level' layout='${level:upperCase=true}'/>
        </layout>
      </layout>
    </target>
  </targets>
  <rules>
  </rules>
</nlog>
```

```json
myAmazingText: { "time": "2016-10-30 13:30:55.0000", "level": "INFO" }
```