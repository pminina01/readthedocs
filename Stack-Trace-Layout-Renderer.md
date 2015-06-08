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
* _separator_ - Stack frame separator string. Default: =>