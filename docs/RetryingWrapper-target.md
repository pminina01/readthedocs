Retries in case of write error. 

Supported in .NET, Silverligt, Compact Framework and Mono.

## Configuration Syntax
```xml
<targets>
  <target xsi:type="RetryingWrapper" name="String" retryDelayMilliseconds="Integer" retryCount="Integer">
    <target xsi:type="wrappedTargetType" ...target properties... />
  </target>
</targets>
```

## Parameters
### General Options
* **name** - Name of the target.

### Retrying Options
* **retryDelayMilliseconds** - Time to wait between retries in milliseconds. Integer Default: 100

* **retryCount** - Number of retries that should be attempted on the wrapped target in case of a failure. Integer Default: 3

### Performance Options
* **OptimizeBufferReuse** - Reduce logging overhead, by allowing buffer reuse. Default: `True`
  > Introduced with NLog v4.4.2. Default became `True` with NLog v4.5