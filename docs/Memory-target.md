Writes log messages to an ArrayList in memory for programmatic retrieval. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```xml
<targets>
  <target xsi:type="Memory" name="String" layout="Layout" />
</targets>
```
Read more about using the [[Configuration File]].

## Parameters
### General Options
* **name** - Name of the target.

### Layout Options
* **layout** - Layout used to format log messages. [Layout](Data-types) Required. Default: `${longdate}|${level:uppercase=true}|${logger}|${message}`

### Performance Options
* **OptimizeBufferReuse** - Reduce logging overhead, by allowing buffer reuse. Default: `True`
  > Introduced with NLog v4.4.2. Default became `True` with NLog v4.5

* **MaxLogsCount** Max count, will remove first if over this threshold.  Introduced with NLog v4.6. 0 means disabled (default) 

## Examples
### Logging to an array
(snippet from    [Memory Simple Example.cs](https://github.com/NLog/NLog/blob/43eca983676d87f1d9d9f28872304236393827ba/examples/targets/Configuration%20API/Memory/Simple/Example.cs)  )

```c#
MemoryTarget target = new MemoryTarget();                                                  
target.Layout = "${message}";                                                              
                                                                                           
NLog.Config.SimpleConfigurator.ConfigureForTargetLogging(target, LogLevel.Debug);          
                                                                                           
Logger logger = LogManager.GetLogger("Example");                                           
logger.Debug("log message");                                                               
                                                                                           
foreach (string s in target.Logs)                                                          
{                                                                                          
    Console.Write("logged: {0}", s);                                                       
}                                                                                          
```

See also [Memory Target Tests](https://github.com/NLog/NLog/blob/43eca983676d87f1d9d9f28872304236393827ba/tests/NLog.UnitTests/Targets/MemoryTargetTests.cs)

### reading from existing target

```
var target = LogManager.Configuration.FindTargetByName<MemoryTarget>("target1");
var logs = target.Logs;
```