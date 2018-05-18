The formatted log message. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${message:exceptionSeparator=String:withException=Boolean:raw=Boolean}
```

## Parameters
### Layout Options
* **exceptionSeparator** - String that separates message from the exception.
* **withException** - Indicates whether to log exception along with message. Boolean
* **raw** - Render the unformatted input message without using input parameters (Useful for structured logging). Boolean
  > Introduced with NLog 4.5

