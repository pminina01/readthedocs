Layout renderers are macros that are used in [Layouts](Layouts).

##Layout Renderers
* ${asp-application} - ASP Application variable.
* ${aspnet-application} - ASP.NET Application variable.
* ${aspnet-request} - ASP.NET Request variable.
* ${aspnet-session} - ASP.NET Session variable.
* ${aspnet-sessionid} - ASP.NET Session ID.
* ${aspnet-user-authtype} - ASP.NET User variable.
* ${aspnet-user-identity} - ASP.NET User variable.
* ${asp-request} - ASP Request variable.
* ${asp-session} - ASP Session variable.
* ${basedir} - The current application domain's base directory.
* ${callsite} - The call site (class name, method name and source information).
* ${counter} - A counter value (increases on each layout rendering).
* ${date} - Current date and time.
* ${document-uri} - URI of the HTML page which hosts the current Silverlight application.
* ${environment} - The environment variable.
* ${event-context} - Log event context data.
* ${exception} - Exception information provided through a call to one of the Logger.*Exception() methods.
* ${file-contents} - Renders contents of the specified file.
* ${gc} - The information about the garbage collector.
* ${gdc} - Global Diagnostics Context item. Provided for compatibility with log4net.
* ${guid} - Globally-unique identifier (GUID).
* ${identity} - Thread identity information (name and authentication information).
* ${install-context} - Installation parameter (passed to InstallNLogConfig).
* ${level} - The log level.
* ${literal} - A string literal.
* ${log4jxmlevent} - XML event description compatible with log4j, Chainsaw and NLogViewer.
* ${logger} - The logger name.
* ${longdate} - The date and time in a long, sortable format yyyy-MM-dd HH:mm:ss.mmm.
* ${machinename} - The machine name that the process is running on.
* ${mdc} - Mapped Diagnostic Context item. Provided for compatibility with log4net.
* ${message} - The formatted log message.
* ${ndc} - Nested Diagnostic Context item. Provided for compatibility with log4net.
* ${newline} - A newline literal.
* ${nlogdir} - The directory where NLog.dll is located.
* ${performancecounter} - The performance counter.
* ${processid} - The identifier of the current process.
* ${processinfo} - The information about the running process.
* ${processname} - The name of the current process.
* ${processtime} - The process time in format HH:mm:ss.mmm.
* ${qpc} - High precision timer, based on the value returned from QueryPerformanceCounter() optionally converted to seconds.
* ${registry} - A value from the Registry.
* ${shortdate} - The short date in a sortable format yyyy-MM-dd.
* ${sl-appinfo} - Information about Silverlight application.
* ${specialfolder} - System special folder path (includes My Documents, My Music, Program Files, Desktop, and more).
* ${stacktrace} - Stack trace renderer.
* ${tempdir} - A temporary directory.
* ${threadid} - The identifier of the current thread.
* ${threadname} - The name of the current thread.
* ${ticks} - The Ticks value of current date and time.
* ${time} - The time in a 24-hour, sortable format HH:mm:ss.mmm.
* ${windows-identity} - Thread Windows identity information (username).

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

##Passing Custom Values to a Layout
Even though the layout renderers provide many pre-defined values, you may need to pass application specific values to your [Layouts](Layouts). You can pass your own values in code by adding custom Properties to the event. You then retrieve the value using the [${event-context}](Event-Context-Layout-Renderer) renderer. See the documentation for the [${event-context}](Event-Context-Layout-Renderer) for an example.