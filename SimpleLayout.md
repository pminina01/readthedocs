Represents a string with embedded placeholders that can render contextual information. 

Supported in .NET, Silverlight, Compact Framework and Mono
##Configuration Syntax
```
<targets>
  <target>
    <layout xsi:type="SimpleLayout">
      <!-- Layout Options -->
      <text>String</text>

    </layout>
  </target>
</targets>
```
##Parameters
###Layout Options
_text_ - Layout text.
##Remarks
This layout is not meant to be used explicitly. Instead you can just use a string containing layout renderers everywhere the layout is required.