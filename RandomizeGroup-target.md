Sends log messages to a randomly selected target. 

Supported in .NET, Silverligt, Compact Framework and Mono.
##Configuration Syntax
```
<targets>
  <target xsi:type="RandomizeGroup" name="String">
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