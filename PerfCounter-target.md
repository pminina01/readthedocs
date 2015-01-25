Increments specified performance counter on each write. 

Supported in .NET and Mono.
##Configuration Syntax
```xml
<targets>
  <target xsi:type="PerfCounter"
          name="String"
          instanceName="String"
          counterHelp="String"
          counterType="Enum"
          autoCreate="Boolean"
          categoryName="String"
          counterName="String" />
</targets>
```
Read more about using the [Configuration File](Configuration-file).
##Parameters
###General Options
_name_ - Name of the target.
###Performance Counter Options
_instanceName_ - Performance counter instance name.

_counterHelp_ - Counter help text.  
> This parameter is not supported in:
> * NLog v1.0 for .NET Framework 1.0
> * NLog v1.0 for .NET Framework 1.1
> * NLog v1.0 for .NET Framework 2.0

_counterType_ - Performance counter type. Default: 65536  
Possible values:
* AverageBase -
* AverageCount64 -
* AverageTimer32 -
* CounterDelta32 -
* CounterDelta64 -
* CounterMultiBase -
* CounterMultiTimer -
* CounterMultiTimer100Ns -
* CounterMultiTimer100NsInverse -
* CounterMultiTimerInverse -
* CounterTimer -
* CounterTimerInverse -
* CountPerTimeInterval32 -
* CountPerTimeInterval64 -
* ElapsedTime -
* NumberOfItems32 -
* NumberOfItems64 -
* NumberOfItemsHEX32 -
* NumberOfItemsHEX64 -
* RateOfCountsPerSecond32 -
* RateOfCountsPerSecond64 -
* RawBase -
* RawFraction -
* SampleBase -
* SampleCounter -
* SampleFraction -
* Timer100Ns -
* Timer100NsInverse -

_autoCreate_ - Indicates whether performance counter should be automatically created.

_categoryName_ - Name of the performance counter category. Required.

_counterName_ - Name of the performance counter. Required.
##Remarks
TODO: 1. Unable to create a category allowing multiple counter instances (.Net 2.0 API only, probably) 2. Is there any way of adding new counters without deleting the whole category? 3. There should be some mechanism of resetting the counter (e.g every day starts from 0), or auto-switching to another counter instance (with dynamic creation of new instance). This could be done with layouts.