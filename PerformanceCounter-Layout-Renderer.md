The performance counter. 

Supported in .NET and Mono.

##Configuration Syntax
```
${performancecounter:category=String:counter=String:instance=String
                    :machineName=String}
```

##Parameters
###Performance Counter Options
* **category** - Name of the counter category. Required.
* **counter** - Name of the performance counter. Required.
* **instance** - Name of the performance counter instance (e.g. this.Global_).
* **machineName** - Name of the machine to read the performance counter from.