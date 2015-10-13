Increments specified performance counter on each write. 

Supported in .NET and Mono.
##Configuration Syntax
```xml
<targets>
  <target xsi:type="PerfCounter"
          counterName="String"
          instanceName="String"
          counterHelp="String"
          counterType="Enum"
          autoCreate="Boolean"
          categoryName="String"
          incrementValue="Layout"
           />
</targets>
```
Read more about using the [Configuration File](Configuration-file).
##Parameters
###General Options
_counterName_ - Name of the counter.
###Performance Counter Options
_instanceName_ - Performance counter instance name.

_counterHelp_ - Counter help text.  

_counterType_ - Performance counter type. Default: `NumberOfItems32`  
Possible values:
* AverageBase
* AverageCount64
* AverageTimer32
* CounterDelta32
* CounterDelta64
* CounterMultiBase
* CounterMultiTimer
* CounterMultiTimer100Ns
* CounterMultiTimer100NsInverse
* CounterMultiTimerInverse
* CounterTimer
* CounterTimerInverse
* CountPerTimeInterval32
* CountPerTimeInterval64
* ElapsedTime
* NumberOfItems32
* NumberOfItems64
* NumberOfItemsHEX32
* NumberOfItemsHEX64
* RateOfCountsPerSecond32
* RateOfCountsPerSecond64
* RawBase
* RawFraction
* SampleBase
* SampleCounter
* SampleFraction
* Timer100Ns
* Timer100NsInverse

_autoCreate_ - Indicates whether performance counter should be automatically created.

_categoryName_ - Name of the performance counter category. Required.

_counterName_ - Name of the performance counter. Required.

_incrementValue_ - Introduced in NLog 4.2. The value by which to increment the counter. [Layout](Layout). Default: 1.