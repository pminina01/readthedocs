Custom Targets, layout etc. could have properties. There are only limitations if you like to set them from the XML config.

The following types are supported

## Allowed types
Allowed types for Targets, Layouts and Layout renderers.

- C# types: e.g. bool, char, decimal, double, float, int, uint, etc.
- Enums (use short name)
- `Encoding`
- `CultureInfo`
- `Type`
- `LineEndingMode` 
- `Uri`
- NLog types: `Layout`, `SimpleLayout` & `ConditionExpression`
- Types which has an implicit conversion from `string`
- Types which are using `TypeDescriptor` from `string` (not Silverlight)
- Collections, introduced in NLog 4.4. See section [Collection types](#user-content-collection-types])




## Collection types
Introduced in NLog 4.4, the following collection types could be used.

Usage in XML: comma separated string. If the value contains a comma, single quote the whole value.

Examples:
- `value="one arg"`
- `value="1,2"`
- `value="value1,'value2,  with comma'"`

Collections of type: 
  -  `IList<T>` / `IList`
  - `IEnumerable<T>` / `IEnumerable` 
  - `ISet<T>` / `HashSet<T>`

with the following types: 
  - C# built in types (string, int, double, object)
  - enum (use short name)
  - culture, encoding, Type
  - not supported: Layout

Not supported:
- Arrays
- Non-generic `List` 
- Non-gereric `IList`
- Custom class implementing/inheriting from the collection classes/interfaces. (because of performance)


PS: .NET 3.5 has `HashSet` but not `ISet`

## XML Elements
For targets and layout renderers there is also support for XML elements.

E.g. the [JSON layout](JsonLayout):

```xml
<target name="jsonFile" xsi:type="File" fileName="${logFileNamePrefix}.json" includeAllProperties="Boolean" excludeProperties="Comma-separated list (string)"   >
      <layout xsi:type="JsonLayout">
              <attribute name="time" layout="${longdate}" />
              <attribute name="level" layout="${level:upperCase=true}"/>
              <attribute name="message" layout="${message}" />
       </layout>
</target>
```

Usage in C#

```c#

[ArrayParameter(typeof(JsonAttribute), "attribute")]
public IList<JsonAttribute> Attributes { get; private set; }

[NLogConfigurationItem]
public class JsonAttribute {} //needs default ctor

```


Another example is the [Database target](Database target)