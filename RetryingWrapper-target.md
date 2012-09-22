Retries in case of write error. 

Supported in .NET, Silverligt, Compact Framework and Mono.
##Configuration Syntax
```
<targets>
  <target xsi:type="RetryingWrapper" name="String" retryDelayMilliseconds="Integer" retryCount="Integer">
    <target xsi:type="wrappedTargetType" ...target properties... />
  </target>
</targets>
```
##Parameters
###General Options
_name_ - Name of the target.
###Retrying Options
_retryDelayMilliseconds_ - Time to wait between retries in milliseconds. Integer Default: 100

_retryCount_ - Number of retries that should be attempted on the wrapped target in case of a failure. Integer Default: 3