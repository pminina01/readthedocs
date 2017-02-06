The current application domain's base directory. 

Supported in .NET, Compact Framework and Mono.

##Configuration Syntax
```
${basedir:dir=String:file=String:processDir=boolean}
```

##Parameters
###Advanced Options
* **dir** - Name of the directory to be Path.Combine()'d with with the base directory.
* **file** - Name of the file to be Path.Combine()'d with with the base directory.
* **processDir** - Introduced in NLog 4.4.2. Render the base directory of the current process? Default `false`. 