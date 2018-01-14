Writes log message to the Event Log. 

Supported in .NET and Mono

## Configuration Syntax
```xml
<targets>
  <target xsi:type="EventLog"
          name="String"
          layout="Layout"
          machineName="String"
          source="Layout" 
          category="Layout"
          eventId="Layout"
          log="String"
          maxKilobytes="long"
          maxMessageLength="Integer" />
<!-- note: source is a string in NLog before 4.0 -->
</targets>
```
Read more about using the [[Configuration File]].

## Parameters
### General Options
* **name** - Name of the target.

### Layout Options
* **layout** - Layout used to format log messages. [Layout](Layouts) Required. Default: `${longdate}|${level:uppercase=true}|${logger}|${message}`. Note: max size of 16384 characters (limitation of the `EventLog` API)

### Performance Options
* **OptimizeBufferReuse** - Reduce logging overhead, by allowing buffer reuse. Default: `True`
  > Introduced with NLog v4.4.2. Default became `True` with NLog v4.5

### Event Log Options
* **machineName** - Name of the machine on which Event Log service is running. Default: `.`  
* **source** - Value to be used as the event Source. By default this is the friendly name of the current AppDomain. From NLog 4.0 this is layoutable(Layouts). 
* **category** - [Layout](Layouts) that renders event Category.  The categories must be predefined for the specified _source_ and needs to be numeric.   
* **eventId** - [Layout](Layouts) that renders event ID. 
* **log** - Name of the Event Log to write to. This can be System, Application or any user-defined name. Default: Application
* **MaxMessageLength** - The message length limit to write to the Event Log. There are [various message length limit that depends on the OS.](https://support.microsoft.com/en-us/kb/957662 "Recommended settings for event log sizes in Windows") Therefore, be careful for the value. Default: 16,384. If given value is zero or negative, then Exception will throw. Introduced in NLog 4.3.
* **onOverflow** - Action to take when a log message is larger than the _MaxMessageLength_ option. Available actions are:
   * _Truncate_ - Truncates the message before writing to the Event Log. This is the default.
   * _Split_ - Splits the message and writes multiple entries to the Event Log. Warning: the message layout will be spread across multiple Event Log entries; if there is an application reading and parsing the Event Log, split messages will not have the expected layout of a log entry.
   * _Discard_ - Discards of the message. It will not be written to the Event Log.
* **MaxKilobytes**  - maximum Event log size in kilobytes. `null` is default (512KB). Value should be multiples of 64 and between 64 and 4194240. Note, this requires admin rights. Introduced in NLog 4.4.10

## Notes
To log to the event log, an event source is required to exist. This involves creating the event source.

When install/uninstalling, the event source is only created / removed when the _source_ doesn't contain layout renderers.

When installing, the event source can only be created when run as an Administrator. Alternatively a simple PowerShell command to create this source is shown below (run PowerShell as Administrator).

    New-EventLog -LogName Application -Source "MySourceName"

The Event Log has a limit in the number of bytes in a message. From [MSDN](https://msdn.microsoft.com/en-us/library/xzwc042w(v=vs.110).aspx#Anchor_1):

> The message string is longer than 31,839 bytes (32,766 bytes on Windows operating systems before Windows Vista).

## Example
```xml
<target xsi:type="EventLog"
            name="eventlog"
            source="test"
            layout="${message}${newline}${exception:format=ToString}"/>
```