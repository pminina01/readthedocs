Stack trace renderer. 

Supported in .NET, Silverlight and Mono

##Configuration Syntax
```
${stacktrace:format=Enum:topFrames=Integer:skipFrames=Integer:separator=String}
```
##Parameters
###Rendering Options
* _format_ - Output format of the stack trace. Default: Flat  
  Possible values:
  * **DetailedFlat** - Detailed flat format (method signatures displayed in a single line).
  * **Flat** - Flat format (class and method names displayed in a single line).
  * **Raw** - Raw format (multiline - as returned by StackFrame.ToString() method).
* _topFrames_ - Number of top stack frames to be rendered. Integer Default: 3
* _skipFrames_ - Numberof frames to skip. Integer Default: 0
* _separator_ - Stack frame separator string. Default: =>. To set new line use `&#13;&#10;`

###Format Examples
**Raw**  
    Main at offset 638 in file:line:column <filename unknown>:0:0  
    TestLogging at offset 590 in file:line:column <filename unknown>:0:0  
    WriteToLog at offset 112 in file:line:column <filename unknown>:0:0  

**Flat**  
    Program.Main  
    Program.TestLogging  
    NLogLoggerHelper.LogEvent   

**DetailedFlat**  
    [Int32 Main()]  
    [Void TestLogging()]  
    [Void WriteToLog(NLog.Logger, NLog.LogLevel, System.String)]   