A specialized layout that renders CSV-formatted events. 

Supported in .NET, Silverlight, Compact Framework and Mono
Configuration Syntax
```xml
<targets>
  <target>
    <layout xsi:type="CsvLayout">
      <!-- Layout Options -->
      <layout xsi:type="layoutType">Layout</layout>
      <footer xsi:type="layoutType">Layout</footer>
      <header xsi:type="layoutType">Layout</header>

      <!-- CSV Options -->
      <quoting>Enum</quoting>
      <quoteChar>String</quoteChar>
      <withHeader>Boolean</withHeader>
      <customColumnDelimiter>String</customColumnDelimiter>
      <delimiter>Enum</delimiter>
      <column layout="Layout" name="String"/> <!-- repeated -->

    </layout>
  </target>
</targets>
```

## Parameters
### Layout Options
* **layout** - Body layout (can be repeated multiple times). Layout

* **footer** - Footer layout. Layout

* **header** - Header layout. Layout

### CSV Options
* **quoting** - Quoting mode. Default: Auto  
Possible values:  
  * All - Quote all column.
  * Auto - Quote only whose values contain the quote symbol or the separator.
  * Nothing - Quote nothing.

**Hint:** To write logs which has multiline data, such as Exception message, you will need to use quotation mark `(")`.

* **quoteChar** - Quote Character. Default: `"`

* **withHeader** - Indicates whether CSV should include header. `Boolean`. Default `true`

* **customColumnDelimiter** - Custom column delimiter value (valid when `ColumnDelimiter` is set to `Custom`).

* **delimiter** - Column delimiter. Default: Auto  
Possible values:  
  * Auto - Automatically detect from regional settings.
  * Comma - Comma (ASCII 44).
  * Custom - Custom string, specified by the `CustomDelimiter`.
  * Pipe - Pipe character (ASCII 124).
  * Semicolon - Semicolon (ASCII 59).
  * Space - Space character (ASCII 32).
  * Tab - Tab character (ASCII 9).

* **columns** - The array of parameters to be passed.Collection  
Each collection item is represented by `<column />` element with the following attributes:  
  * _layout_ - Layout of the column.Layout Required.
  * _name_ - Name of the column.

## Example

```xml
<target xsi:type="File" fileName="${csvPath}">
    <layout xsi:type="CsvLayout" delimiter="Tab" withHeader="false">
        <column name="time" layout="${longdate}" />
        <column name="level" layout="${level:upperCase=true}"/>
        <column name="message" layout="${message}" />
        <column name="callsite" layout="${callsite:includeSourcePath=true}" />
        <column name="stacktrace" layout="${stacktrace:topFrames=10}" />
        <column name="exception" layout="${exception:format=ToString}"/>
        <column name="property1" layout="${event-properties:property1}"/>

    </layout>
</target>
```
