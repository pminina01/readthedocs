The information about the running process. 

Supported in .NET

## Configuration Syntax
```
${processinfo:property=Enum:format=string}
```

## Parameters
### Rendering Options
* **property** - Property to retrieve. Default: **Id**  
  Possible values:  
  * _ExitCode_ - Exit Code.
  * _ExitTime_ - Exit Time.
  * _Handle_ - Process Handle.
  * _HandleCount_ - Handle Count.
  * _HasExited_ - Whether process has exited.
  * _Id_ - Process ID.
  * _MachineName_ - Machine name.
  * _MainWindowHandle_ - Handle of the main window.
  * _MainWindowTitle_ - Title of the main window.
  * _MaxWorkingSet_ - Maximum Working Set.
  * _MinWorkingSet_ - Minimum Working Set.
  * _NonPagedSystemMemorySize_ - Non-paged System Memory Size.
  * _NonPagedSystemMemorySize64_ - Non-paged System Memory Size (64-bit).
  * _PagedMemorySize_ - Paged Memory Size.
  * _PagedMemorySize64_ - Paged Memory Size (64-bit)..
  * _PagedSystemMemorySize_ - Paged System Memory Size.
  * _PagedSystemMemorySize64_ - Paged System Memory Size (64-bit).
  * _PeakPagedMemorySize_ - Peak Paged Memory Size.
  * _PeakPagedMemorySize64_ - Peak Paged Memory Size (64-bit).
  * _PeakVirtualMemorySize_ - Peak Virtual Memory Size.
  * _PeakVirtualMemorySize64_ - Peak Virtual Memory Size (64-bit)..
  * _PeakWorkingSet_ - Peak Working Set Size.
  * _PeakWorkingSet64_ - Peak Working Set Size (64-bit).
  * _PriorityBoostEnabled_ - Whether priority boost is enabled.
  * _PriorityClass_ - Priority Class.
  * _PrivateMemorySize_ - Private Memory Size.
  * _PrivateMemorySize64_ - Private Memory Size (64-bit).
  * _PrivilegedProcessorTime_ - Privileged Processor Time.
  * _ProcessName_ - Process Name.
  * _Responding_ - Whether process is responding.
  * _SessionId_ - Session ID.
  * _StartTime_ - Process Start Time.
  * _TotalProcessorTime_ - Total Processor Time.
  * _UserProcessorTime_ - User Processor Time.
  * _VirtualMemorySize_ - Virtual Memory Size.
  * _VirtualMemorySize64_ - Virtual Memory Size (64-bit).
  * _WorkingSet_ - Working Set Size.
  * _WorkingSet64_ - Working Set Size (64-bit)

* **format** formatstring in the value is formatable. Ex. formatting process StartTime. Introduced in NLog 4.4
