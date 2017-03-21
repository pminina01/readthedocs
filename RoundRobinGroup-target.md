Distributes log events to targets in a round-robin fashion. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
<targets>
  <target xsi:type="RoundRobinGroup" name="String">
    <target xsi:type="wrappedTargetType" ... />
    <target xsi:type="wrappedTargetType" ... />
    ...
    <target xsi:type="wrappedTargetType" ... />
  </target>
</targets>
```

## Parameters
### General Options
* **name** - Name of the target.