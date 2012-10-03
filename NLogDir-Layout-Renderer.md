The directory where NLog.dll is located. 

Supported in .NET, Compact Framework and Mono.

##Configuration Syntax
```
${nlogdir:dir=String:file=String}
```

##Parameters
###Advanced Options
* **dir** - Name of the directory to be Path.Combine()'d with the directory name.
* **file** - Name of the file to be Path.Combine()'d with the directory name.