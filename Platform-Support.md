## General
Feature|.NET 3.5|.NET 4.0|.NET 4.5|NetStandard 1.3|Xamarin iOs|Xamarin Android|Mono|WP8|Silverlight|Remarks	
 -----| -----| -----| -----| -----| -----| -----| -----| -----| -----| -----	
read app.config/web.config|✓ |✓ |✓ |✓ |||✓ |||	
autoloading .dll|✓ |✓ |✓ |±|✓ |✓ |✓ |||±: expected 	
auto reload|✓ |✓ |✓ |✓ |||✓ |||	
stacktrace with source|✓ |✓ |✓ ||✓ |✓ |✓ |||	
fluent interface|||✓ |✓ |||?|||	
NLogTraceListener|✓ |✓ |✓ ||||✓ |||	
	
## Layout Renderers
Layout Renderer|.NET 3.5|.NET 4.0|.NET 4.5|NetStandard|Xamarin iOs|Xamarin Android|Mono|WP8|Silverlight|Remarks	
 -----| -----| -----| -----| -----| -----| -----| -----| -----| -----| -----	
AllEventProperties|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ | Include Caller Information: .NET 4.5 only	
AppDomain|✓ |✓ |✓ ||✓ |✓ |✓ |||	
AspApplicationValue|✓ |✓ |✓ |||||||	
AspRequestValue|✓ |✓ |✓ |||||||	
AspSessionValue|✓ |✓ |✓ |||||||	
AssemblyVersion|✓ |✓ |✓ |1.5+|✓ |✓ |✓ |✓ |✓ |	
BaseDir|✓ |✓ |✓ |✓ |✓ |✓ |✓ |||	
CallSite|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |±|±: no file name or source path	
CallSiteLineNumber|✓ |✓ |✓ |✓ |✓ |✓ |✓ |||	
Counter|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
Date|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
DocumentUri|||||||||✓ |	
Environment|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ ||	
EventContext|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
EventProperties|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
Exception|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |±|±: no method name	
FileContents|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
GarbageCollectorInfo|✓ |✓ |✓ |✓ |✓ |✓ ||✓ |±|±: no collection count option	
Gdc|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
Guid|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
Identity|✓ |✓ |✓ ||✓ |✓ |✓ |||	
InstallContext|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
Level|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
Literal|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
Log4JXmlEvent|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |±|±: no file name or source path	
LoggerName|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
LongDate|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
MachineName|✓ |✓ |✓ |✓|✓ |✓ |✓ |✓ ||	
Mdc|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
Mdlc||✓ |✓ |✓||||||	
Message|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
NewLine|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
NLogDir|✓ |✓ |✓ |1.5+|✓ |✓ |✓ |||	
Ndc|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
NewLine|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
PerformanceCounter|✓ |✓ |✓ ||||✓ |||	
ProcessId|✓ |✓ |✓ |✓||✓ |✓ |||	
ProcessInfo|✓ |✓ |✓ |✓|✓ |✓ ||||	
ProcessName|✓ |✓ |✓ |✓||✓ |✓ |||	
ProcessTime|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
QueryPerformanceCounter|✓ |✓ |✓ ||||✓ |||	
Registry|✓ |✓ |✓ ||||✓ |||	
ShortDate|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
SilverlightApplicationInfo|||||||||✓ |	
SpecialFolder|✓ |✓ |✓ ||✓ |✓ |✓ |✓ |✓ |	
StackTrace|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
TempDir|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
ThreadId|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
ThreadName|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
Ticks|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
Time|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
TraceActivityId|✓ |✓ |✓ ||✓ |✓ |✓ |||	
Variable|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
WindowsIdentity|✓ |✓ |✓ |✓ |✓ |✓ |✓ |||	

## Layout renderer (wrapped)
Layout renderer|.NET 3.5|.NET 4.0|.NET 4.5|NetStandard 1.3|Xamarin iOs|Xamarin Android|Mono|WP8|Silverlight|Remarks	
 -----| -----| -----| -----| -----| -----| -----| -----| -----| -----| -----	
Cached|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
FileSystemNormalize|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
JsonEncode|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
Lowercase|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
OnException|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
Padding|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
Replace|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
ReplaceNewLines|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
Rot13|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
TrimWhiteSpace|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
Uppercase|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
UrlEncode|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
WrapLine|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
WhenEmpty|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
XmlEncode|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	

## Targets
Target|.NET 3.5|.NET 4.0|.NET 4.5|NetStandard 1.3|Xamarin iOs|Xamarin Android|Mono|WP8|Silverlight|Remarks	
 -----| -----| -----| -----| -----| -----| -----| -----| -----| -----| -----	
AspResponse|✓ |✓ |✓ |||||||	
Chainsaw|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
ColoredConsole|✓ |✓ |✓ |±|||✓ |||±: no encoding	
Console|✓ |✓ |✓ |±|±|±|✓ |±|±|±: no encoding	
Database|✓ |✓ |✓ |±|||✓ |||	±: no transactions or reading from .config
Debug|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
Debugger|✓ |✓ |✓ ||✓ |✓ |✓ |✓ |✓ |	
EventLog|✓ |✓ |✓ ||||✓ |||	
File|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
LogReceiverWebService|✓ |✓ |✓ ||||✓ ||✓ |	
Mail|✓ |✓ |✓ ||✓ |✓ |✓ |||	
Memory|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
MethodCall|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
NLogViewer|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |±|±: no UDP	
Network|✓ |✓ |✓ |✓|✓ |✓ |✓ |✓ |✓ |	
Null|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
OutputDebugString|✓ |✓ |✓ |✓ |||✓ |||	
PerformanceCounter|✓ |✓ |✓ ||||✓ |||	
Trace|✓ |✓ |✓ |✓ |✓ |✓ |✓ |||	
WebService|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	

## Target-wrappers
Target|.NET 3.5|.NET 4.0|.NET 4.5|NetStandard 1.3|Xamarin iOs|Xamarin Android|Mono|WP8|Silverlight|Remarks	
 -----| -----| -----| -----| -----| -----| -----| -----| -----| -----| -----	
AsyncWrapper |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
AutoFlushWrapper |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
BufferingWrapper |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
FilteringWrapper |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
FallbackGroup |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
FilteringWrapper |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
ImpersonatingWrapper |✓ |✓ |✓ ||||✓ |||	
LimitingWrapper |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
PostFilteringWrapper |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
RandomizeGroup |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
RepeatingWrapper |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
RetryingWrapper |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
RoundRobinGroup|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
SplitGroup|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |	
