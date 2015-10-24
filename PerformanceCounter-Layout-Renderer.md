The performance counter. 

Supported in .NET and Mono.

##Configuration Syntax
```
${performancecounter:CategoryName=String:CounterName=String:InstanceName=String
                    :machineName=String:AutoCreate:Boolean:CounterType=PerformanceCounterType:IncrementValue=Integer}
```

##Parameters
###Performance Counter Options
* **CategoryName** - Name of the counter category. Required.
* **CounterName** - Name of the performance counter. Required.
* **InstanceName** - Name of the performance counter instance (e.g. this.Global_).
* **machineName** - Name of the machine to read the performance counter from.
* **CounterType** - The performance counter type. Default NumberOfItems32. Possible options, see [MSDN](https://msdn.microsoft.com/en-us/library/system.diagnostics.performancecountertype(v=vs.110).aspx). 
* **IncrementValue** Value to increment the counter. Default 1.