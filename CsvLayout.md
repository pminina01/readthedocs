A specialized layout that renders CSV-formatted events. 

Supported in .NET, Silverlight, Compact Framework and Mono
Configuration Syntax
```
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
##Parameters
##Layout Options
_layout_ - Body layout (can be repeated multiple times). Layout

_footer_ - Footer layout. Layout

_header_ - Header layout. Layout
###CSV Options
_quoting_ - Quoting mode. Default: Auto  
Possible values:  
* All - Quote all column.
* Auto - Quote only whose values contain the quote symbol or the separator.
* Nothing - Quote nothing.

_quoteChar_ - Quote Character. Default: "

_withHeader_ - Indicates whether CSV should include header.Boolean

_customColumnDelimiter_ - Custom column delimiter value (valid when ColumnDelimiter is set to 'Custom').

_delimiter_ - Column delimiter. Default: Auto  
Possible values:  
* Auto - Automatically detect from regional settings.
* Comma - Comma (ASCII 44).
* Custom - Custom string, specified by the CustomDelimiter.
* Pipe - Pipe character (ASCII 124).
* Semicolon - Semicolon (ASCII 59).
* Space - Space character (ASCII 32).
* Tab - Tab character (ASCII 9).

_columns_ - The array of parameters to be passed.Collection  
Each collection item is represented by \<column /> element with the following attributes:  
  * _layout_ - Layout of the column.Layout Required.
  * _name_ - Name of the column.