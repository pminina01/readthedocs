Render Stack trace of a log event. 

Supported in .NET, Silverlight and Mono

## Configuration Syntax
```
${stacktrace:format=Enum:topFrames=Integer:skipFrames=Integer:separator=String}
```

## Parameters
### Rendering Options
* **format** - Output format of the stack trace. Default: Flat  
  Possible values:
  * _DetailedFlat_ - Detailed flat format (method signatures displayed in a single line).
  * _Flat_ - Flat format (class and method names displayed in a single line).
  * _Raw_ - Raw format (multiline - as returned by StackFrame.ToString() method).
* **topFrames** - Number of top stack frames to be rendered. Integer Default: 3
* **skipFrames** - Numberof frames to skip. Integer Default: 0
* **separator** - Stack frame separator string. Default: =>. To set new line use `&#13;&#10;`

## Examples

### Raw

Note: To get the filenames and line numbers, include the PDB files. 

Note: Prior NLog 4.4.7, the result was always `<filename unknown>:0:0  `

    Main at offset 638 in file:line:column file1.cs:100:10  
    TestLogging at offset 590 in file:line:column testlogger.cs:30:10  
    WriteToLog at offset 112 in file:line:column testlogger.cs:10:20

### Flat
    Program.Main  
    Program.TestLogging  
    NLogLoggerHelper.LogEvent   

### DetailedFlat
    [Int32 Main()]  
    [Void TestLogging()]  
    [Void WriteToLog(NLog.Logger, NLog.LogLevel, System.String)]   