##General
Feature|.NET 3.5|.NET 4.0|.NET 4.5|Xamarin iOs|Xamarin Android|Mono|WP8|Silverlight|Remarks
 -----| -----| -----| -----| -----| -----| -----| -----| -----| -----
read app.config/web.config|✓ |✓ |✓ |||✓ |||
autoloading .dll|✓ |✓ |✓ |✓ |✓ |✓ |||
auto reload|✓ |✓ |✓ |||✓ |||
stacktrace with source|✓ |✓ |✓ |✓ |✓ |✓ |||
fluent interface|||✓ |||?|||

##Layout Renderers
Layout Renderer|.NET 3.5|.NET 4.0|.NET 4.5|Xamarin iOs|Xamarin Android|Mono|WP8|Silverlight|Remarks
 -----| -----| -----| -----| -----| -----| -----| -----| -----| -----
AllEventProperties|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ | Include Caller Information: .NET 4.5 only
AppDomain|✓ |✓ |✓ |✓ |✓ |✓ |✓ ||
AspApplicationValue|✓ |✓ |✓ ||||||
AspRequestValue|✓ |✓ |✓ ||||||
AspSessionValue|✓ |✓ |✓ ||||||
AssemblyVersion|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
BaseDir|✓ |✓ |✓ |✓ |✓ |✓ |✓ ||
CallSite|✓ |✓ |✓ |✓ |✓ |✓ |✓ |±|±: no file name or source path
CallSiteLineNumber|✓ |✓ |✓ |✓ |✓ |✓ |✓ ||
Counter|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Date|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
DocumentUri||||||||✓ |
Environment|✓ |✓ |✓ |✓ |✓ |✓ |✓ ||
EventContext|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
EventProperties|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Exception|✓ |✓ |✓ |✓ |✓ |✓ |✓ |±|±: no method name
FileContents|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
GarbageCollectorInfo|✓ |✓ |✓ |✓ |✓ ||✓ |±|±: no collection count option
Gdc|✓ |✓ |✓ |✓ |✓ |✓ |✓ ||
Guid|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Identity|✓ |✓ |✓ |✓ |✓ |✓ |✓ ||
InstallContext|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Level|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Literal|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Log4JXmlEvent|✓ |✓ |✓ |✓ |✓ |✓ |✓ |±|±: no file name or source path
LoggerName|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
LongDate|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
MachineName|✓ |✓ |✓ |✓ |✓ |✓ |✓ ||
Mdc|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Mdlc||✓ |✓ ||||||
Message|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
NLogDir|✓ |✓ |✓ |✓ |✓ |✓ |✓ ||
Ndc|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
NewLine|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
PerformanceCounter|✓ |✓ |✓ |||✓ |✓ ||
ProcessId|✓ |✓ |✓ ||✓ |✓ |✓ ||
ProcessInfo|✓ |✓ |✓ |✓ |✓ ||✓ ||
ProcessName|✓ |✓ |✓ ||✓ |✓ |✓ ||
ProcessTime|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
QueryPerformanceCounter|✓ |✓ |✓ ||✓ |✓ |||
Registry|✓ |✓ |✓ |||✓ |✓ ||
ShortDate|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
SilverlightApplicationInfo||||||||✓ |
SpecialFolder|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
StackTrace|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
TempDir|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
ThreadId|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
ThreadName|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Ticks|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Time|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
TraceActivityId|✓ |✓ |✓ |✓ |✓ |✓ |✓ ||
Variable|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
WindowsIdentity|✓ |✓ |✓ |✓ |✓ |✓ |✓ ||

##Layout renderer (wrapped)
Layout renderer|.NET 3.5|.NET 4.0|.NET 4.5|Xamarin iOs|Xamarin Android|Mono|WP8|Silverlight|Remarks
 -----| -----| -----| -----| -----| -----| -----| -----| -----| -----
Cached|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
FileSystemNormalize|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
JsonEncode|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Lowercase|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
OnException|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Padding|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Replace|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
ReplaceNewLines|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Rot13|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
TrimWhiteSpace|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Uppercase|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
UrlEncode|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
WhenEmpty|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
XmlEncode|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |

##Targets
Target|.NET 3.5|.NET 4.0|.NET 4.5|Xamarin iOs|Xamarin Android|Mono|WP8|Silverlight|Remarks
 -----| -----| -----| -----| -----| -----| -----| -----| -----| -----
AspResponse|✓ |✓ |✓ ||||||
Chainsaw|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
ColoredConsole|✓ |✓ |✓ |||✓ |||
Console|✓ |✓ |✓ |±|±|✓ |✓ |±|±: no encoding
Database|✓ |✓ |✓ |||✓ |✓ ||
Debug|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Debugger|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
EventLog|✓ |✓ |✓ |||✓ |||
File|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
LogReceiverWebService|✓ |✓ |✓ |||✓ ||✓ |
Mail|✓ |✓ |✓ |✓ |✓ |✓ |✓ ||
Memory|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
MethodCall|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
NLogViewer|✓ |✓ |✓ |✓ |✓ |✓ |✓ |±|±: no UDP
Network|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Null|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
OutputDebugString|✓ |✓ |✓ ||✓ |✓ |✓ ||
PerformanceCounter|✓ |✓ |✓ |||✓ |✓ ||
Trace|✓ |✓ |✓ |✓ |✓ |✓ |✓ ||
WebService|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |

##Target-wrappers
Target|.NET 3.5|.NET 4.0|.NET 4.5|Xamarin iOs|Xamarin Android|Mono|WP8|Silverlight|Remarks
 -----| -----| -----| -----| -----| -----| -----| -----| -----| -----
Async|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
AutoFlush|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Buffering|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
FallbackGroup|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
FilteringRule.cs|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Filtering|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Impersonating|✓ |✓ |✓ ||✓ |✓ |✓ ||
PostFiltering|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
RandomizeGroup|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Repeating|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
Retrying|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
RoundRobinGroup|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
SplitGroup|✓ |✓ |✓ |✓ |✓ |✓ |✓ |✓ |
