High precision timer, based on the value returned from QueryPerformanceCounter() optionally converted to seconds. 

Supported in .NET, Compact Framework and Mono.

## Configuration Syntax
```
${qpc:normalize=Boolean:difference=Boolean:alignDecimalPoint=Boolean
     :precision=Integer:seconds=Boolean}
```

## Parameters
### Rendering Options
* **normalize** - Indicates whether to normalize the result by subtracting it from the result of the first call (so that it's effectively zero-based). Boolean Default: True
* **difference** - Indicates whether to output the difference between the result of QueryPerformanceCounter and the previous one. Boolean Default: False
* **alignDecimalPoint** - Indicates whether to align decimal point (emit non-significant zeros). Boolean Default: True
* **precision** - Number of decimal digits to be included in output. Integer Default: 4
* **seconds** - Indicates whether to convert the result to seconds by dividing by the result of QueryPerformanceFrequency(). Boolean Default: True