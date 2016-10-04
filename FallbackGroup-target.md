Provides fallback-on-error. 

Supported in .NET, Silverlight, Compact Framework and Mono.
##Configuration Syntax
```xml
<targets>
  <target xsi:type="FallbackGroup" name="String" returnToFirstOnSuccess="Boolean">
    <target xsi:type="wrappedTargetType" ... />
    <target xsi:type="wrappedTargetType" ... />
    ...
    <target xsi:type="wrappedTargetType" ... />
  </target>
</targets>
```
##Parameters
###General Options
_name_ - Name of the target.
###Fallback Options
_returnToFirstOnSuccess_ - Indicates whether to return to the first target after any successful write. `Boolean`. Default `false`