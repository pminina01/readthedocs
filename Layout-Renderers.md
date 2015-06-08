Layout renderers are template macros that are used in [Layouts](Layouts).

##Layout Renderers
* [${all-event-properties}](All-Event-Properties-Layout-Renderer) - Log all event context data.
* [${appdomain}](AppDomain-Layout-Renderer) - Current app domain. 
* [${appsetting}](AppSetting-Layout-Renderer) - App config setting.
* [${asp-application}](AspApplication-Layout-Renderer) - ASP Application variable.
* [${aspnet-application}](AspNetApplication-Layout-Renderer) - ASP.NET Application variable.
* [${aspnet-request}](AspNetRequest-Layout-Renderer) - ASP.NET Request variable.
* [${aspnet-session}](AspNetSession-Layout-Renderer) - ASP.NET Session variable.
* [${aspnet-sessionid}](AspNetSessionId-Layout-Renderer) - ASP.NET Session ID.
* [${aspnet-user-authtype}](AspNetUserAuthType-Layout-Renderer) - ASP.NET User variable.
* [${aspnet-user-identity}](AspNetUserIdentity-Layout-Renderer) - ASP.NET User variable.
* [${asp-request}](AspRequest-Layout-Renderer) - ASP Request variable.
* [${asp-session}](AspSession-Layout-Renderer) - ASP Session variable.
* [${assembly-version}](AssemblyVersion-Layout-Renderer) - The version of the executable in the default application domain.
* [${basedir}](Basedir-Layout-Renderer) - The current application domain's base directory.
* [${callsite}](Callsite-Layout-Renderer) - The call site (class name, method name and source information).
* [${callsite-linenumber}](Callsite-line-number-layout-renderer) - The call site source line number.
* [${counter}](Counter-Layout-Renderer) - A counter value (increases on each layout rendering).
* [${date}](Date-Layout-Renderer) - Current date and time.
* [${document-uri}](DocumentUri-Layout-Renderer) - URI of the HTML page which hosts the current Silverlight application.
* [${environment}](Environment-Layout-Renderer) - The environment variable.
* [${event-context}](EventContext-Layout-Renderer) - Log event context data.
* [${exception}](Exception-Layout-Renderer) - Exception information provided through a call to one of the Logger.*Exception() methods.
* [${file-contents}](FileContents-Layout-Renderer) - Renders contents of the specified file.
* [${gc}](Gc-Layout-Renderer) - The information about the garbage collector.
* [${gdc}](Gdc-Layout-Renderer) - Global Diagnostic Context item. Provided for compatibility with log4net.
* [${guid}](Guid-Layout-Renderer) - Globally-unique identifier (GUID).
* [${identity}](Identity-Layout-Renderer) - Thread identity information (name and authentication information).
* [${install-context}](InstallContext-Layout-Renderer) - Installation parameter (passed to InstallNLogConfig).
* [${level}](Level-Layout-Renderer) - The log level.
* [${literal}](Literal-Layout-Renderer) - A string literal.
* [${log4jxmlevent}](Log4JXMLEvent-Layout-Renderer) - XML event description compatible with log4j, Chainsaw and NLogViewer.
* [${logger}](Logger-Layout-Renderer) - The logger name.
* [${longdate}](LongDate-Layout-Renderer) - The date and time in a long, sortable format yyyy-MM-dd HH:mm:ss.mmm.
* [${machinename}](MachineName-Layout-Renderer) - The machine name that the process is running on.
* [${mdc}](Mdc-Layout-Renderer) - Mapped Diagnostic Context item. Provided for compatibility with log4net.
* [${message}](Message-Layout-Renderer) - The formatted log message.
* [${ndc}](Ndc-Layout-Renderer) - Nested Diagnostic Context item. Provided for compatibility with log4net.
* [${newline}](Newline-Layout-Renderer) - A newline literal.
* [${nlogdir}](NLogDir-Layout-Renderer) - The directory where NLog.dll is located.
* [${performancecounter}](PerformanceCounter-Layout-Renderer) - The performance counter.
* [${processid}](ProcessId-Layout-Renderer) - The identifier of the current process.
* [${processinfo}](ProcessInfo-Layout-Renderer) - The information about the running process.
* [${processname}](ProcessName-Layout-Renderer) - The name of the current process.
* [${processtime}](ProcessTime-Layout-Renderer) - The process time in format HH:mm:ss.mmm.
* [${qpc}](QPC-Layout-Renderer) - High precision timer, based on the value returned from QueryPerformanceCounter() optionally converted to seconds.
* [${registry}](Registry-Layout-Renderer) - A value from the Registry.
* [${shortdate}](ShortDate-Layout-Renderer) - The short date in a sortable format yyyy-MM-dd.
* [${sl-appinfo}](Sl-AppInfor-Layout-Renderer) - Information about Silverlight application.
* [${specialfolder}](Special-Folder-Layout-Renderer) - System special folder path (includes My Documents, My Music, Program Files, Desktop, and more).
* [${stacktrace}](Stack-Trace-Layout-Renderer) - Stack trace renderer.
* [${tempdir}](TempDir-Layout-Renderer) - A temporary directory.
* [${threadid}](ThreadId-Layout-Renderer) - The identifier of the current thread.
* [${threadname}](ThreadName-Layout-Renderer) - The name of the current thread.
* [${ticks}](Ticks-Layout-Renderer) - The Ticks value of current date and time.
* [${time}](Time-Layout-Renderer) - The time in a 24-hour, sortable format HH:mm:ss.mmm.
* [${windows-identity}](Windows-Identity-Layout-Renderer) - Thread Windows identity information (username).

##Wrapper Layout Renderers
* [${cached}](Cached-Layout-Renderer) - Applies caching to another layout output.
* [${filesystem-normalize}](Filesystem-Normalize-Layout-Renderer) - Filters characters not allowed in the file names by replacing them with safe character.
* [${json-encode}](Json-Encode-Layout-Renderer) - Escapes output of another layout using JSON rules.
* [${lowercase}](Lowercase-Layout-Renderer) - Converts the result of another layout output to lower case.
* [${onexception}](OnException-Layout-Renderer) - Only outputs the inner layout when exception has been defined for log message.
* [${pad}](Pad-Layout-Renderer) - Applies padding to another layout output.
* [${replace}](Replace-Layout-Renderer) - Replaces a string in the output of another layout with another string.
* [${rot13}](Rot13-Layout-Renderer) - Decodes text "encrypted" with ROT-13.
* [${trim-whitespace}](Trim-Whitespace-Layout-Renderer) - Trims the whitespace from the result of another layout renderer.
* [${uppercase}](Uppercase-Layout-Renderer) - Converts the result of another layout output to upper case.
* [${url-encode}](Url-Encode-Layout-Renderer) - Encodes the result of another layout output for use with URLs.
* [${when}](When-Layout-Renderer) - Only outputs the inner layout when the specified condition has been met.
* [${whenEmpty}](WhenEmpty-Layout-Renderer) - Outputs alternative layout when the inner layout produces empty result.
* [${xml-encode}](Xml-Encode-Layout-Renderer) - Converts the result of another layout output to be XML-compliant.

##Custom Layout Renderers
* [${gelf}](https://github.com/farzadpanahi/NLog.GelfLayout) - Converts log to [GELF](http://www.graylog2.org/resources/gelf) format.

##Passing Custom Values to a Layout
Even though the layout renderers provide many pre-defined values, you may need to pass application specific values to your [Layouts](Layouts). You can pass your own values in code by adding custom Properties to the event. You then retrieve the value using the [${event-context}](Event-Context-Layout-Renderer) renderer. See the documentation for the [${event-context}](Event-Context-Layout-Renderer) for an example.