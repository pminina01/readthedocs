A specialized layout that renders Log4j-compatible XML events. 

Supported in .NET, Silverligt, Compact Framework and Mono
##Configuration Syntax
```
<targets>
  <target>
    <layout xsi:type="Log4JXmlEventLayout">
    </layout>
  </target>
</targets>
```
##Remarks
This layout is not meant to be used explicitly. Instead you can use ${log4jxmlevent} layout renderer.