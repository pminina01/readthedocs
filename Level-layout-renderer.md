The [log level](Log-Levels). 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${level}
```
Alternatively, add padding to align the message.
```
${pad:padding=5:inner=${level:uppercase=true}}
```

## Examples
### Basic
Configuration:
```
${level}
```
Code:
```
logger.Debug("Test Message")
```
Result:
```
Debug
```