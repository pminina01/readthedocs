Filters buffered log entries based on a set of conditions that are evaluated on a group of events. 

Supported in .NET, Silverligt, Compact Framework and Mono.
##Configuration Syntax
```xml
<targets>
  <target xsi:type="PostFilteringWrapper" name="String" defaultFilter="Condition">
    <target xsi:type="wrappedTargetType" ...target properties... />
    <when exists="Condition" filter="Condition"/><!-- repeated -->
  </target>
</targets>
```
##Parameters
###General Options
_name_ - Name of the target.
###Filtering Options
_defaultFilter_ - Default filter to be applied when no specific rule matches. Condition
###Filtering Rules
_rules - The collection of filtering rules. The rules are processed top-down and the first rule that matches determines the filtering condition to be applied to log events. Collection  
Each collection item is represented by \<when /> element with the following attributes:  
* _exists_ - Condition to be tested. Condition Required.
* _filter_ - Resulting filter to be applied when the condition matches. Condition Required.

##Remarks
PostFilteringWrapper must be used with some type of buffering target or wrapper, such as AsyncTargetWrapper, BufferingWrapper or ASPNetBufferingWrapper.