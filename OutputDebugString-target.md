Outputs log messages through the [OutputDebugString](https://msdn.microsoft.com/da-dk/library/windows/desktop/aa363362.aspx) Win32 API. That can be monitored using [DebugView](https://docs.microsoft.com/en-us/sysinternals/downloads/debugview).

Supported in .NET Framework, Mono and NetStandard
> NetStandard translates into [System.Diagnostics.Debug.WriteLine](https://msdn.microsoft.com/en-us/library/system.diagnostics.debug.writeline.aspx)

## Configuration Syntax
```xml
<targets>
  <target xsi:type="OutputDebugString" name="String" layout="Layout" />
</targets>
```
Read more about using the [[Configuration File]].

## Parameters
### General Options
* **name** - Name of the target.

### Layout Options
* **layout** - Layout used to format log messages. Required. Default: `${longdate}|${level:uppercase=true}|${logger}|${message}`

### Performance Options
* **OptimizeBufferReuse** - Reduce logging overhead, by allowing buffer reuse. Default: `True`
  > Introduced with NLog v4.4.2. Default became `True` with NLog v4.5

### See Also
There is similar [Debugger-target](https://github.com/NLog/NLog/wiki/Debugger-target), that  writes to [System.Diagnostics.Debugger.Log](https://msdn.microsoft.com/en-us/library/system.diagnostics.debugger.log.aspx) - Posts a message for the attached debugger.  