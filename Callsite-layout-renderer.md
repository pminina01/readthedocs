The call site (class name, method name and source information). 

Supported in .NET, Silverlight and Mono.

##Configuration Syntax
```
${callsite:className=Boolean:includeNamespace=Boolean:fileName=Boolean:includeSourcePath=Boolean
          :methodName=Boolean:cleanNamesOfAnonymousDelegates=Boolean:skipFrames=Integer}
```

##Parameters
###Rendering Options
* **className** - Indicates whether to render the class name.Boolean Default: `True`
* **includeNamespace** - Include namespace in class name? Introduced in NLog 4.4. Default: `True`
* **fileName** - Indicates whether to render the source file name and line number.Boolean Default: `False`
* **includeSourcePath** - Indicates whether to include source file path.Boolean Default: `True`
* **methodName** - Indicates whether to render the method name.Boolean Default: `True`
* **cleanNamesOfAnonymousDelegates** - Indicates whether the method name will be cleaned up if it is detected as an anonymous delegate. Boolean Default: `False`
* **skipFrames** - The number of frames to skip. Integer Default: `0`


##Notes
please note that the method name won't work well with async methods before NLog 4.3 - it will always show `MoveNext`. 