Buffers log events for the duration of ASP.NET request and sends them down to the wrapped target at the end of a request. 

Supported in .NET and Mono

## Configuration Syntax
```xml
<targets>
  <target xsi:type="AspNetBufferingWrapper"
          name="String"
          bufferGrowLimit="Integer"
          growBufferAsNeeded="Boolean"
          bufferSize="Integer">
    <target xsi:type="wrappedTargetType" ...target properties... />
  </target>
</targets>
```

## Parameters

### General Options
* **name** - Name of the target.

### Buffering Options
* **bufferGrowLimit** - Maximum number of log events that the buffer can keep. Integer

* **growBufferAsNeeded** - Indicates whether buffer should grow as needed. Boolean Default: False  
Value of true causes the buffer to expand until BufferGrowLimit is hit, false causes the buffer to never expand and lose the earliest entries in case of overflow.

* **bufferSize** - Number of log events to be buffered. Integer Default: 100

## Remarks
Typically this target is used in cooperation with PostFilteringTargetWrapper to provide verbose logging for failing requests and normal or no logging for successful requests. We need to make the decision of the final filtering rule to apply after all logs for a page have been generated. To use this target, you need to add an entry in the httpModules section of web.config: 
```
<?xml version="1.0" ?>
 <configuration>
  <system.web>
   <httpModules>
    <add name="NLog" type="NLog.Web.NLogHttpModule, NLog.Web"/>
   </httpModules>
 </system.web>
</configuration>
```