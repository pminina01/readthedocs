Sends log messages through System.Diagnostics.Trace. 

Supported in .NET and Mono.

## Configuration Syntax
```xml
<targets>
  <target xsi:type="Trace" name="String" layout="Layout" />
</targets>
```

## Parameters
### General Options
* **name** - Name of the target.
### Layout Options
* **layout** - Layout used to format log messages. Layout Required. Default: `${longdate}|${level:uppercase=true}|${logger}|${message}`
* **rawWrite** - Always use `Trace.WriteLine` independent of LogLevel. Default: `False`
  > Introduced with NLog 4.5, fixes the issue with output being prefixed with exe-filename. And helps Azure Streaming log.
### Performance Options
* **OptimizeBufferReuse** - Reduce logging overhead, by allowing buffer reuse. Default: `True`
  > Introduced with NLog v4.4.2. Default became `True` with NLog v4.5