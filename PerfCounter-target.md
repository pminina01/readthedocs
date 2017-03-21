Increments specified performance counter on each write. 

Supported in .NET and Mono.

## Configuration Syntax
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
Read more about using the [[Configuration File]].

## Parameters
### General Options
* **counterName** - Name of the counter.

### Performance Counter Options
* **instanceName** - Performance counter instance name.

* **counterHelp** - Counter help text.  

* **counterType** - Performance counter type. Default: `NumberOfItems32`  
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

* **autoCreate** - Indicates whether performance counter should be automatically created.

* **categoryName** - Name of the performance counter category. Required.

* **counterName** - Name of the performance counter. Required.

* **incrementValue** - Introduced in NLog 4.2. The value by which to increment the counter. Layout. Default: 1.