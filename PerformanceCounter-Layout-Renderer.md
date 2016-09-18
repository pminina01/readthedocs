The performance counter. 

Supported in .NET and Mono.

##Configuration Syntax
```
${performancecounter:Category=String:Counter=PerformanceCounterType:Instance=String
                    :IncrementValue=Integer:MachineName:string}
```

##Parameters
###Performance Counter Options
* **Category** - Name of the counter category. Required.
* **Counter** - The performance counter type. Default NumberOfItems32. Possible options, see [MSDN](https://msdn.microsoft.com/en-us/library/system.diagnostics.performancecountertype(v=vs.110).aspx). Required.
* **Instance** - Name of the performance counter instance (e.g. this.Global_).
* **IncrementValue** Value to increment the counter. Default 1. Introduced in NLog 4.2
* **MachineName**  The name of the machine to read the performance counter from.