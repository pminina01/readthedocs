##Possible causes
When you get no log output from NLog, this can be because of the following reasons:
 1. NLog cannot find the configuration file
 2. Configuration file is invalid
 3. Logging rules are incorrect or no rules are defined
 4. Application tracing code is incorrect.
 5. There is a runtime problem with the target (such as missing permissions)
 6. Logs are written to a different location.

##Troubleshooting steps
 1. The first step is to make sure that NLog finds your config file. It is recommended to use NLog.config located in the same directory as your application, but there are other options. See [NLog Configuration](Configuration-file) for more information. Once you've made sure that the configuration file is there, proceed to the next step.
 2. Configuration file is read when you create your first Logger, so the best way to validate that your configuration file is syntactically valid is to create one in the Main() method of your program.
```csharp
class Program
{
    static void Main()
    {
        Logger logger = LogManager.GetLogger("foo");
    }
}
```
When troubleshooting, it is advised to turn on exceptions, so that NLog will report any problems to the calling application. This can be done in one of two ways:
  * In config file add `throwExceptions="true"` to the root element, so that it looks like this:
```
<nlog throwExceptions="true">
   ...
</nlog>
```
  * You can also set `LogManager.ThrowExceptions` to true at the beginning of your program:
```csharp
class Program
{
    static void Main()
    {
        LogManager.ThrowExceptions = true;
        Logger logger = LogManager.GetLogger("foo");
    }
}
```
Now, when loading the configuration file, you should see exception being raised.
 3. To eliminate the possibility that your logging rules are incorrect, add the rule which matches all loggers and all levels at the beginning of your \<rules> section.
```
<nlog throwExceptions="true">
  <targets>
    <target name="file" type="File" fileName="${basedir}/log.txt" />
  </targets>
  <rules>
    <logger name="*" minLevel="Trace" writeTo="{all target names separated by comma}" />
  </rules>
</nlog>
```
 4. If it still does not work, there is a possiblity is that the code in your application may be incorrect. To make sure this is not the case, add the following code to your `Main()` method:
```csharp
class Program
{
    static void Main()
    {
        Logger logger = LogManager.GetLogger("foo");
        logger.Info("Program started"); 
    }
}
```
 5. If there is any problem with the target your're using (such as insufficient permissions when writing to a file), you should get an exception explaining the problem right from the place where the problem occured.
 6. If after following steps 1..5 you still don't see your log messages - there is another possibility: your log files may be written to a different location. If you don't use a fully qualified name of the file (such as c:\logs\log.txt, or ${basedir}\log.txt your logs may be written to the working directory, which is not necessarily the same directory as where the application resides.

##Internal Logging
NLog has its own [internal logging](Internal-logging) system which can be used to troubleshoot problems with log routing and configuration. The simplest way to enable is to add the following attributes to your configuration file:

* `internalLogFile="c:\path\to\internal_log_file.txt"` - specifies the location of the internal log file
* `internalLogLevel="Trace"` specifies the level of detail of information written to the internal log file
* `internalLogToConsole="true"` writes internal log to the console output
More ways to enable internal logging are explained [here](Internal-logging).

##Other troubleshooting tools and techniques
You may use a tracing application such as [Process Monitor](http://technet.microsoft.com/en-us/sysinternals/bb896645.aspx) from SysInternals to monitor file activity in your system. This should give you an idea of what files are being read and written and their exact locations.

[Process Explorer](http://technet.microsoft.com/en-us/sysinternals/bb896653.aspx) is another indispensable utility which can help with investigation of various system-level issues, such as permissions, threading, deadlocks, performance, etc.