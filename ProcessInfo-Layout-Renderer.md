The information about the running process. 

Supported in .NET

##Configuration Syntax
```
${processinfo:property=Enum}
```

##Parameters
###Rendering Options
* _property_ - Property to retrieve. Default: Id  
  Possible values:  
  * **BasePriority** - Base Priority.
  * **ExitCode** - Exit Code.
  * **ExitTime** - Exit Time.
  * **Handle** - Process Handle.
  * **HandleCount** - Handle Count.
  * **HasExited** - Whether process has exited.
  * **Id** - Process ID.
  * **MachineName** - Machine name.
  * **MainModule** -

    > This parameter is not supported in:
    > * NLog v2.0 for .NET Framework 2.0
    > * NLog v2.0 for .NET Framework 3.5
    > * NLog v2.0 for .NET Framework 4.0


  * **MainWindowHandle** - Handle of the main window.
  * **MainWindowTitle** - Title of the main window.
  * **MaxWorkingSet** - Maximum Working Set.
  * **MinWorkingSet** - Minimum Working Set.
  * **NonpagedSystemMemorySize** -

    > This parameter is not supported in:
    > * NLog v2.0 for .NET Framework 2.0
    > * NLog v2.0 for .NET Framework 3.5
    > * NLog v2.0 for .NET Framework 4.0

  * **NonPagedSystemMemorySize** - Non-paged System Memory Size.

    > This parameter is not supported in:
    > * NLog v1.0 for .NET Framework 1.0
    > * NLog v1.0 for .NET Framework 1.1
    > * NLog v1.0 for .NET Framework 2.0

  * **NonpagedSystemMemorySize64** -

    > This parameter is not supported in:
    > * NLog v2.0 for .NET Framework 2.0
    > * NLog v2.0 for .NET Framework 3.5
    > * NLog v2.0 for .NET Framework 4.0

  * **NonPagedSystemMemorySize64** - Non-paged System Memory Size (64-bit).

    > This parameter is not supported in:
    > * NLog v1.0 for .NET Framework 1.0
    > * NLog v1.0 for .NET Framework 1.1
    > * NLog v1.0 for .NET Framework 2.0

  * **PagedMemorySize** - Paged Memory Size.
  * **PagedMemorySize64** - Paged Memory Size (64-bit)..
  * **PagedSystemMemorySize** - Paged System Memory Size.
  * **PagedSystemMemorySize64** - Paged System Memory Size (64-bit).
  * **PeakPagedMemorySize** - Peak Paged Memory Size.
  * **PeakPagedMemorySize64** - Peak Paged Memory Size (64-bit).
  * **PeakVirtualMemorySize** - Peak Vitual Memory Size.
  * **PeakVirtualMemorySize64** - Peak Virtual Memory Size (64-bit)..
  * **PeakWorkingSet** - Peak Working Set Size.
  * **PeakWorkingSet64** - Peak Working Set Size (64-bit).
  * **PriorityBoostEnabled** - Whether priority boost is enabled.
  * **PriorityClass** - Priority Class.
  * **PrivateMemorySize** - Private Memory Size.
  * **PrivateMemorySize64** - Private Memory Size (64-bit).
  * **PrivilegedProcessorTime** - Privileged Processor Time.
  * **ProcessName** - Process Name.
  * **Responding** - Whether process is responding.
  * **SessionId** - Session ID.
  * **StartTime** - Process Start Time.
  * **TotalProcessorTime** - Total Processor Time.
  * **UserProcessorTime** - User Processor Time.
  * **VirtualMemorySize** - Virtual Memory Size.
  * **VirtualMemorySize64** - Virtual Memory Size (64-bit).
  * **WorkingSet** - Working Set Size.
  * **WorkingSet64** - Working Set Size (64-bit).