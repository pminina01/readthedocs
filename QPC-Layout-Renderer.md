High precision timer, based on the value returned from QueryPerformanceCounter() optionally converted to seconds. 

Supported in .NET, Compact Framework and Mono.

##Configuration Syntax
```
${qpc:normalize=Boolean:difference=Boolean:alignDecimalPoint=Boolean
     :precision=Integer:seconds=Boolean}
```

##Parameters
###Rendering Options
* _normalize_ - Indicates whether to normalize the result by subtracting it from the result of the first call (so that it's effectively zero-based). Boolean Default: True

  > This parameter is not supported in:
  > * NLog v1.0 for .NET Compact Framework 1.0
  > * NLog v1.0 for .NET Compact Framework 2.0
  > * NLog v1.0 for .NET Framework 1.0
  > * NLog v1.0 for .NET Framework 1.1
  > * NLog v1.0 for .NET Framework 2.0

* _difference_ - Indicates whether to output the difference between the result of QueryPerformanceCounter and the previous one. Boolean Default: False

  > This parameter is not supported in:
  > * NLog v1.0 for .NET Compact Framework 1.0
  > * NLog v1.0 for .NET Compact Framework 2.0
  > * NLog v1.0 for .NET Framework 1.0
  > * NLog v1.0 for .NET Framework 1.1
  > * NLog v1.0 for .NET Framework 2.0

* _alignDecimalPoint_ - Indicates whether to align decimal point (emit non-significant zeros). Boolean Default: True
* _precision_ - Number of decimal digits to be included in output. Integer Default: 4
* _seconds_ - Indicates whether to convert the result to seconds by dividing by the result of QueryPerformanceFrequency(). Boolean Default: True