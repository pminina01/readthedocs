The [log level](Log-Levels). 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${level:format=Enum}
```
Alternatively, add padding to align the message.
```
${pad:padding=5:inner=${level:uppercase=true}}
```

## Parameters
* **format** - Output format of the level. Introduced in 4.4.6 Default: Name  
  Possible values:
  * _Name_ - Render the full level name.
  * _FirstCharacter_ - Render the first character of the level.
  * _Ordinal_ - Render the ordinal (aka number) for the level.

  | Level | FirstCharacter | Ordinal |
  | ----- | -------------- | ------- |
  | Trace | T              | 0
  | Debug | D              | 1
  | Info  | I              | 2
  | Warn  | W              | 3
  | Error | E              | 4
  | Fatal | F              | 5
  | Off   | O              | 6

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

### Format
Configuration:
```
${level:format=FirstCharacter}
```
Code:
```
logger.Debug("Test Message")
```
Result:
```
D
```