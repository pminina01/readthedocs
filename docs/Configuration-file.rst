
Configuration file
==================

This page describes how to configure NLog via XML specification.


.. contents:: Table of Contents

File locations
--------------

At startup, NLog searches for its configuration in various files as
described below. It loads the first nlog configuration found. Search
ends when the first nlog configuration is found. NLog fails if no
configuration is found.

For a stand-alone *.exe application, files are searched as follows:*
standard application configuration file (usually
applicationname.exe.config)
* applicationname.exe.nlog in application’s
directory
* NLog.config in application’s directory (*Name sensitive;
using docker dotnet core*)
* NLog.dll.nlog in a directory where
NLog.dll is located (only if NLog isn’t installed in the GAC)

For an ASP.NET application, files are searched as follows:
* standard
web application file web.config
* web.nlog located in the same
directory as web.config
* NLog.config in application’s directory
*
NLog.dll.nlog in a directory where NLog.dll is located (only if NLog
isn’t installed in the GAC)

For the .NET Compact Framework – which doesn’t recognize application
configuration files (*.exe.config) or environmental variables, files are
searched as follows:* applicationname.exe.nlog in application’s
directory
* NLog.config in application’s directory
* NLog.dll.nlog in
a directory where NLog.dll is located (only if NLog isn’t installed in
the GAC)

For Xamarin Android, the assets folder is supported. “NLog.config” in
the assets folder will be loaded automatically. If the file name is
different, then use:

.. code:: c#

   LogManager.Configuration = new XmlLoggingConfiguration("assets/someothername.config");

File layout
-----------

NLog configuration is formatted as XML and is either embedded in a
Visual Studio project config file (app.config or web.config) or is a
stand-alone XML file.

To embed in a project config file, add an nlog ``section`` element under
``configSections`` and add an ``nlog`` element. For example:

.. code:: xml

   <configuration>
     <configSections>
       <section name="nlog" type="NLog.Config.ConfigSectionHandler, NLog"/>
     </configSections>
     ...
     <nlog>
     ...
     </nlog>
   </configuration>

As a stand-alone file, the root element is ``nlog``. For example:

.. code:: xml

   <nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
   ...
   </nlog>

The use of an XML namespace is optional, but enables Intellisense in
Visual Studio.

NLog config is case-insensitive when **not** using a namespace and is
case-sensitive when using a namespace.

Top-level elements
------------------

You can use the following elements as children to ``nlog``. ``targets``
and ``rules`` are required in any configuration The others are optional
and can be useful in advanced scenarios.
- ``targets`` – defines log
targets/outputs
* ``rules`` – defines log routing rules
*
``extensions`` – loads NLog extensions from the *.dll file* ``include``–
includes external configuration file
* ``variable`` – sets the value of
a configuration variable

The simplest configuration consists of one ``target`` and one rule
(``logger``) that routes messages to the target.

Targets
-------

The ``targets`` section defines log `Targets <Targets>`__. Each target
is represented by a ``target`` element. There are two attributes
required for each target:
* ``name`` – target name
* ``type`` – target
type – such as “File”, “Database”, “Mail”. When using namespaces this
attribute is named ``xsi:type``.

In addition to these attributes, targets usually accept other
parameters, which impact the way diagnostic traces are written. Each
target has a different set of parameters, they are described in detail
on project’s homepage and they are context-sensitive. Intellisense is
also available in Visual Studio.

For example – the `File target <File-target>`__ accepts the ``fileName``
parameter which defines output file name and the `Console
target <Console-target>`__ has the ``error`` parameter which determines
whether the diagnostic traces are written to standard error (stderr)
instead of standard output (stdout) of the process.

This example demonstrates a ``targets`` section which defines multiple
targets: two files, one network target and OutputDebugString target:

.. code:: xml

   <targets>
     <target name="f1" xsi:type="File" fileName="file1.txt"/>
     <target name="f2" xsi:type="File" fileName="file2.txt"/>  
     <target name="n1" xsi:type="Network" address="tcp://localhost:4001"/>
     <target name="ds" xsi:type="OutputDebugString"/>
   </targets>

NLog provides many predefined `Targets <Targets>`__. It’s actually very
easy to create your own target - see `How to write a custom
Target <How-to-write-a-custom-target>`__.

Rules
-----

The ``rules`` section maps loggers to `targets <#targets>`__ and `log
levels <#log-levels>`__.

A rule is a ``logger`` element with the following attributes:

-  ``name`` – logger name pattern - may include wildcard characters (\*
   and ?)
-  ``minlevel`` – minimal level to log
-  ``maxlevel`` – maximum level to log
-  ``level`` – single level to log
-  ``levels`` - comma separated list of levels to log
-  ``writeTo`` – comma separated list of targets to write to
-  ``final`` – no rules are processed after a final rule matches
-  ``enabled`` - set to ``false`` to disable the rule without deleting
   it

Note: Although a rule is named ``logger``, it does not *define* a
logger. It *references* one or more loggers.

| A rule is mapped to a logger by matching the rule ``name`` pattern to
  a logger name. A rule ``name`` attribute may include wildcard
  characters (\* and ?) to match logger names by wildcard matching.
|
* ``*`` - matches 0 or more characters
* ``?`` - matches exactly 1
  character

Until NLog 4.6, are allowed only wildcards (*) at the beginning and/or
at the end of the pattern.

.. code:: xml

   <rules>
     <logger name="*" minlevel="Info" writeTo="logconsole" />
     <logger name="Name.Space.*" minlevel="Debug" writeTo="f1" />  
     <logger name="*.Class1" minlevel="Trace" writeTo="f2" />
     <logger name="*.Library.*" minlevel="Warn" writeTo="f3" />
   </rules>

Since NLog 4.6, wildcards (\* and ?) are allowed in any position.

.. code:: xml

   <rules>
     <logger name="*TcpTestServer[*].Connection[07].*" minlevel="Trace" writeTo="logconsole" final="true" />
     <logger name="*TcpTestServer[*].Connection[??].*" minlevel="Debug" writeTo="logconsole" final="true" />
     <logger name="*" minlevel="Info" writeTo="logconsole" />
   </rules>

Rules are processed in sequential order. Multiple rules may apply to a
logger. Use ``final`` to stop processing rules after a match is found.

A rule defines which log entry level(s) are logged. Entries with other
levels are ignored. A commonly used specifier is ``minLevel``. The other
specifiers allow for more advanced configuration.

If a rule contains more than one level-declaring attribute (``level``,
``levels``, ``minLevel`` and ``maxLevel``) only the first
level-declaring attribute or set is used and the rest are ignored.

The level-declaring attributes are processed in the following order:

1. ``level``
2. ``levels``
3. ``minlevel`` and ``maxlevel`` (these have the same priority)
4. *none* (all levels are logged)

[Need clarification: Is the *sequentially* first level-related attribute
used? Or is the first *processed* used? For example, given
“minLevel=Warn level=Info”, which is used?]

In case a rule is marked as ``final`` and contains any level-declaring
attributes, the ``final`` attribute applies only to the specified
levels.

Example rules
-------------

.. code:: xml

   <logger name="Name.Space.Class1" minlevel="Debug" writeTo="f1" />

Configures messages from the logger named “Name.Space.Class1” with level
``Debug`` and higher to be written to the “f1” target.

A logger can have any name, but in this case it was created by class
“Class1” which is in namespace “Name.Space”. See
``LogManager.GetCurrentClassLogger()``.

.. code:: xml

   <logger name="Name.Space.Class1" levels="Debug,Error" writeTo="f1" />

Configures messages from the logger named “Name.Space.Class1” with level
``Debug`` or ``Error`` to be written to the “f1” target.

.. code:: xml

   <logger name="Name.Space.*" writeTo="f3,f4" />

Configures messages from any class in the “Name.Space” namespace to be
written to both “f3” and “f4” targets regardless of level.

.. code:: xml

   <logger name="Name.Space.*" minlevel="Debug" maxlevel="Error" final="true" />
   <logger name="*" writeTo="f1" />

Configures to ignore messages from any class in the ``Name.Space``
namespace with level between ``Debug`` and ``Error`` (which is
``Debug``, ``Info``, ``Warn``, ``Error``). The first rule selects
loggers, but since there is no ``writeTo``, these messages are not
logged. And, since this rule contains ‘final=true’, the last rule does
not apply to loggers matching the first rule.

Include files
-------------

NLog provides an include file feature so that configuration can be
stored in multiple files.

.. code:: xml

   <include file="nlog-common.config" />

Like most attributes in NLog config, the file attribute may reference
variables. The following example includes a file named the same as the
machine that nlog is running on.

.. code:: xml

   <include file="${machinename}.config"/>

Set the attribute ``ignoreErrors`` to ``true`` to prevent a startup
failure if the include file cannot be loaded – file not found, invalid
XML, …. Use the `Troubleshooting logging <#troubleshooting-logging>`__
section to log errors. This attribute is optional and defaults to
``false``.

Since NLog 4.4.2, wildcards (``*``) are allowed. E.g.
``<include file="nlog-*.config"/>``

A larger example can be found here: `XML config <include />
example <XML-config-include-example>`__

Variables
---------

Variables allow you to enhance configuration by accessing environment
information and to simplify configuration by reducing repeated text.
NLog defines variables that you can use in your configuration. Also, you
can define and use custom variables.

Define a custom variable as follows:

.. code:: xml

   <variable name="varname" value="xxx" />

The value of a variable can be inserted into an attribute value via the
``${varname}`` syntax. A variable value can even be used to define the
value another variable. The following example shows using a pre-defined
variable ``shortdate`` and defining and using a custom variable
``logDirectory``.

.. code:: xml

   <nlog>
     <variable name="logDirectory" value="logs/${shortdate}"/>
     <targets>
       <target name="file1" xsi:type="File" fileName="${logDirectory}/file1.txt"/>
       <target name="file2" xsi:type="File" fileName="${logDirectory}/file2.txt"/>
     </targets>
   </nlog>

With this syntax, a variable must be defined before use. Otherwise
configuration initialization will fail.

NLog 4.1 introduced a new syntax for using a variable value. See
`Variable layout
renderer <Var-Layout-Renderer>`__.

.. code:: xml

   ${var:varname}

This syntax provides the following advantages over the older syntax:

-  Variables can be changed, deleted and created from the API
-  A default value can be configured for a variable,
   e.g. \ ``${var:password:default=unknown}``
-  By default, variables are reset when the configuration reloads. In
   order to take the variables from current configuration, add
   ``keepVariablesOnReload="true"`` to the ``nlog`` element (introduced
   in NLog 4.4).

Layouts and layout renderers
----------------------------

One of NLog’s strongest assets is the ability to use
`layouts <Layouts>`__. In the simplest form, layouts are texts with
embedded tags delimited by ``${`` and ``}``. The tags are called `Layout
Renderers <Layout-Renderers>`__ and can be used to insert pieces of
contextual information into the text.

Layouts can be used in many places, for example they can control the
format of information written on the screen or sent to a file, but also
to control the file names themselves. This is very powerful, which we’ll
see in a moment.

Let’s assume, that we want to annotate each message written to the
console with: 

* current date and time 
* name of the class and method that emitted the log message 
* log level 
* message text

This is very easy:

.. code:: xml

   <target name="c" xsi:type="Console"  layout="${longdate} ${callsite} ${level} ${message}"/>

We can make each messages for each logger go to a separate file, as in
the following example:

.. code:: xml

   <target name="f" xsi:type="File" fileName="${logger}.txt"/>

As you can see, the ${logger} layout renderer was used in the fileName
attribute, which causes each log message to be written to the file whose
name includes the logger name. The above example will create the
following files:
* Name.Space.Class1.txt
* Name.Space.Class2.txt
* Name.Space.Class3.txt
* Other.Name.Space.Class1.txt
* Other.Name.Space.Class2.txt
* Other.Name.Space.Class3.txt

Log levels
----------

Each log entry has a level. And each logger is configured to include or
ignore certain levels. A common configuration is to specify the minimum
level where that level and higher levels are included. For example, if
the minimum level is Info, then Info, Warn, Error and Fatal are logged,
but Debug and Trace are ignored.

The log levels, in descending order, are as follows:

----- ------------------------------------------------------------------
Level Typical Use
----- ------------------------------------------------------------------
Fatal Something bad happened; application is going down
Error Something failed; application may or may not continue
Warn  Something unexpected; application will continue
Info  Normal behavior like mail sent, user updated profile etc.
Debug For debugging; executed query, user authenticated, session expired
Trace For trace debugging; begin method X, end method X
----- ------------------------------------------------------------------

There is one more level, Off. Since it is the highest value and is not
used for entries, it disables logging when used as the minimum log
level.

Automatic reconfiguration
-------------------------

The configuration file is read automatically at program startup. In a
long running process (such as a Windows service or an ASP.NET
application) it’s sometimes desirable to temporarily increase the log
level without stopping the application. NLog can monitor logging
configuration files and re-read them each time they are modified. To
enable this mechanism, you simply add ``autoReload="true"`` parameter to
the configuration file.

.. code:: xml

   <nlog autoReload="true">
      ...
   </nlog>

Note that automatic reconfiguration supports include files, so each time
one of the included files is changed, the entire configuration gets
reloaded.

*Just to make it explicit, automatic reloading will NOT stop/recycle the
IIS Application Pool.*

Troubleshooting logging
-----------------------

Sometimes our application doesn’t write anything to the log files, even
though we have supposedly configured logging properly. There can be many
reasons for logs not being written. The most common problems are
permissions issues, usually in an ASP.NET process, where the
``aspnet_wp.exe`` or ``w3wp.exe`` process may not have write access to
the directory where we want to store logs.

NLog is designed to swallow run-time exceptions that may result from
logging. The following settings can change this behavior and/or redirect
these messages.
* ``<nlog throwExceptions="true" />`` - adding the
``throwExceptions`` attribute in the config file causes NLog to stop
masking exceptions and pass them to the calling application instead.
This attribute is useful at deployment time to quickly locate any
problems. It’s recommended to set ``throwExceptions`` to ``"false"`` as
soon as the application is properly configured to run, so that any
accidental logging problems won’t crash the application.
*
``<nlog throwConfigExceptions="true" />`` - the same as
``throwExceptions`` but for configuration exceptions. If not set (or
``null``), this is the same value as ``throwExceptions``. Introduced in
NLog 4.3. Default ``null`` (so same value as ``throwExceptions``)
*
``<nlog internalLogFile="file.txt" />`` - adding ``internalLogFile``
causes NLog to write its internal debugging messages to the specified
file. This includes any exceptions that may be thrown during logging.
*
``<nlog internalLogLevel="Trace|Debug|Info|Warn|Error|Fatal" />`` –
determines the internal log level. The higher the level, the less
verbose the internal log output.
*
``<nlog internalLogToConsole="false|true" />`` – determines whether
internal logging messages are sent to the console.
*
``<nlog internalLogToConsoleError="false|true" />`` – determines whether
internal logging messages are sent to the console error output (stderr).
\* ``<nlog internalLogToTrace="false|true" />`` – determines whether
internal logging messages are sent to the ``System.Diagnostics.Trace``,
which can be easily viewed in Visual Studio.

Asynchronous processing and wrapper targets
-------------------------------------------

NLog provides wrapper and compound targets which modify other targets’
behavior by adding features like:
* asynchronous processing (wrapped
target runs in a separate thread)
* retry-on-error
* load balancing
*
buffering
* filtering
* failover (failover)

To define a wrapper in the configuration file, simply nest a target node
within another target node. You can even wrap a wrapper target - there
are no limits on depth. For example, to add asynchronous logging with
retry-on-error functionality add this to your configuration file:

.. code:: xml

   <targets>
     <target name="n" xsi:type="AsyncWrapper">
       <target xsi:type="RetryingWrapper">
         <target xsi:type="File" fileName="${file}.txt" />
       </target>
     </target>
   </targets>

Because asynchronous processing is a common scenario, NLog supports a
shorthand notation to enable it for all targets without the need to
specify explicit wrappers. You can simply set ``async="true"`` on
targets element and all your targets within that element will be wrapped
with the ``AsyncWrapper`` target.

.. code:: xml

   <nlog>
     <targets async="true">
       <!-- all targets in this section will automatically be asynchronous -->
     </targets>
   </nlog>

Default wrappers
----------------

Sometimes we require ALL targets to be wrapped in the same way, for
example to add buffering and/or retrying. NLog provides
``<default-wrapper />`` syntax for that. You simply put this element in
the ``<targets />`` section and all your targets will be automatically
wrapped with the specified wrapper. Note that ``<default-wrapper />``
applies to the single ``<targets />`` section only and you can have
multiple sections so you can define groups of targets that are wrapped
in a similar manner.

.. code:: xml

   <nlog>  
     <targets>  
       <default-wrapper xsi:type="BufferingWrapper" bufferSize="100"/>  
       <target name="f1" xsi:type="File" fileName="f1.txt"/>  
       <target name="f2" xsi:type="File" fileName="f2.txt"/>  
     </targets>  
     <targets>  
       <default-wrapper xsi:type="AsyncWrapper">  
         <wrapper-target xsi:type="RetryingWrapper"/>  
       </default-wrapper>  
       <target name="n1" xsi:type="Network" address="tcp://localhost:4001"/>  
       <target name="n2" xsi:type="Network" address="tcp://localhost:4002"/>  
       <target name="n3" xsi:type="Network" address="tcp://localhost:4003"/>  
     </targets>  
   </nlog>

In the above example we’ve defined two buffered File targets and three
asynchronous and retrying Network targets.

Default target parameters
-------------------------

Similar to default wrappers, NLog provides
``<default-target-parameters />`` which enables you to specify default
values of target parameters. For example, if you don’t want files to be
kept open, you can either add ``keepFileOpen="false"`` to each target,
as in the following example:

.. code:: xml

   <nlog>
     <targets>
       <target name="f1" xsi:type="File" fileName="f1.txt" keepFileOpen="false"/>
       <target name="f2" xsi:type="File" fileName="f2.txt" keepFileOpen="false"/>
       <target name="f3" xsi:type="File" fileName="f3.txt" keepFileOpen="false"/>
      </targets>
   </nlog>

Alternatively you can specify a single ``<default-target-parameters />``
that applies to all targets in the ``<targets />`` section. Default
parameters are defined on a per-type basis and are applied BEFORE the
actual attributes defined in the XML file:

.. code:: xml

   <nlog>
     <targets>
       <default-target-parameters xsi:type="File" keepFileOpen="false"/>
       <target name="f1" xsi:type="File" fileName="f1.txt"/>
       <target name="f2" xsi:type="File" fileName="f2.txt"/>
       <target name="f3" xsi:type="File" fileName="f3.txt"/>
     </targets>
   </nlog>

Content escaping
----------------

In the configuration file some characters needs to be escaped. Because
it XML file, the ``<`` and ``>`` brackets should be escaped with
``&lt;`` and ``&gt;``. This also holds for the attribute values, like a
condition.

Inside a layout we need to escape the ``}`` bracket and the colon ``:``
should be escaped because:

-  ``:`` is the value separator.
-  ``}`` is the end of the layout

Nested layout renderers doesn’t need escaping. Also the backslash
doesn’t need an escape.

Examples:

-  ``${appdomain:format={1\}{0\}}`` (escape of ``}``)
-  ``${rot13:inner=${ndc:topFrames=3:separator=x}}`` (no escaping
   needed)
-  ``${when:when=1 -- 1:Inner=Test\: Hello}`` (escape of ``:``)

Extensions
----------

Extensions can be configured to include additional NLog packages or
custom ones:

Just reference the DLL in the config in the ``<extensions />`` as shown
below. The name should not include the ``.dll``

Configuration file example:

.. code:: xml

   <nlog> 
     <extensions> 
       <add assembly="MyAssembly"/> 
     </extensions> 
     <targets> 
       <target name="a1" type="MyFirst" host="localhost"/> 
     </targets> 
     <rules> 
       <logger name="*" minLevel="Info" appendTo="a1"/> 
     </rules> 
   </nlog>

Starting from NLog 4.0 assemblies with the name "NLog*.dll“, like
“NLog.CustomTarget.dll” are now loaded automatically. This assembly
should be in the same folder as ``NLog.dll``.
