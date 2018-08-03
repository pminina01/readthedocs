Writes log messages to one or more files. 

Since NLog 4.3 the `${basedir}` isn't needed anymore for relative paths.

Supported in .NET, Silverlight, Compact Framework and Mono.
## Configuration Syntax
```xml
<targets>
  <target xsi:type="File"
          name="String"
          layout="Layout"
          header="Layout"
          footer="Layout"
          encoding="Encoding"
          lineEnding="Enum"
          archiveAboveSize="Long"
          maxArchiveFiles="Integer"
          archiveFileName="Layout"
          archiveNumbering="Enum"
          archiveDateFormat="String"
          archiveEvery="Enum"          
          archiveOldFileOnStartup="Boolean"
          replaceFileContentsOnEachWrite="Boolean"
          fileAttributes="Enum"
          fileName="Layout"
          deleteOldFileOnStartup="Boolean"
          enableFileDelete="Boolean"
          createDirs="Boolean"
          concurrentWrites="Boolean"
          openFileFlushTimeout="Integer"
          openFileCacheTimeout="Integer"
          openFileCacheSize="Integer"
          networkWrites="Boolean"
          concurrentWriteAttemptDelay="Integer"
          concurrentWriteAttempts="Integer"
          bufferSize="Integer"
          autoFlush="Boolean"
          keepFileOpen="Boolean"
          forceManaged="Boolean"
          enableArchiveFileCompression="Boolean"
          cleanupFileName="Boolean"
          writeFooterOnArchivingOnly="Boolean"
          writeBom="Boolean" />
</targets>
```
Read more about using the [Configuration File](Configuration-file).
## Parameters
### General Options
* **name** - Name of the target.

* **forceManaged** - Indicates that the file target should only use managed methods. This disables some of the options.

### Layout Options
* **layout** - Text to be rendered. [Layout](Layouts) Required. Default: `${longdate}|${level:uppercase=true}|${logger}|${message}`

* **header** - Header. [Layout](Layouts)  

* **footer** - Footer. [Layout](Layouts)

* **encoding** - File encoding name like "utf-8", "ascii" or "utf-16". See [Encoding class on MSDN](http://msdn.microsoft.com/en-us/library/system.text.encoding%28v=vs.110%29.aspx). Defaults to `Encoding.Default` (`UTF-8` on silverlight)

* **writeBom** - Indicates whether to write BOM (byte order mark) in created files. [Boolean](Data-types) Default: False. Introduced in NLog 4.5

* **lineEnding** - Line ending mode.  
Possible values:
  * CR - Insert CR character (ASCII 13) after each line.
  * CRLF - Insert CR LF sequence (ASCII 13, ASCII 10) after each line.
  * Default - Insert platform-dependent end-of-line sequence after each line.
  * LF - Insert LF character (ASCII 10) after each line.
  * None - Don't insert any line ending.

### Archival Options
* **archiveAboveSize** - Size in bytes above which log files will be automatically archived. [Long](Data-types#long)  
Caution: Enabling this option can considerably slow down your file logging in multi-process scenarios. If only one process is going to be writing to the file, consider setting ConcurrentWrites to false for maximum performance. 
**Warning: combining this mode with _Archive Numbering Date_ is not supported. Archive files are not merged. _DateAndSequence_ will work**
 
* **maxArchiveFiles** - Maximum number of archive files that should be kept. If _maxArchiveFiles_ is less or equal to 0, old files aren't deleted [Integer](Data-types#integer) Default: 0  

* **archiveFileName** - Name of the file to be used for an archive. [Layout](Layouts)  
It may contain a special placeholder {#####} that will be replaced with a sequence of numbers depending on the archiving strategy. The number of hash characters used determines the number of numerical digits to be used for numbering files.  
**warning** when deleting archives files is enabled (e.g. _maxArchiveFiles_ ), the folder of the archives should different than the log files.

* **archiveNumbering** - Way file archives are numbered. See also [Archive Numbering Examples](#archive-numbering-examples)   
Possible values:
  * Rolling - Rolling style numbering (the most recent is always #0 then #1, ..., #N).
  * Sequence - Sequence style numbering. The most recent archive has the highest number.
  * Date - Date style numbering. The date is formatted according to the value of _archiveDateFormat_. **Warning: combining this mode with _archiveAboveSize_ is not supported. Archive files are not merged.  **
  * DateAndSequence - Combination of _Date_ and _Sequence_ .Archives will be stamped with the prior period (Year, Month, Day) datetime.
     The most recent archive has the highest number (in combination with the date). The date is formatted according to the value of _archiveDateFormat_.

* **archiveEvery** - Indicates whether to automatically archive log files every time the specified time passes.  
Possible values:
  * Day - Archive daily.
  * Hour - Archive every hour.
  * Minute - Archive every minute.
  * Month - Archive every month.
  * None - Don't archive based on time.
  * Year - Archive every year.
  * Sunday - Archive every Sunday. Introduced in NLog 4.4.4.
  * Monday - Archive every Monday. Introduced in NLog 4.4.4.
  * Tuesday - Archive every Tuesday. Introduced in NLog 4.4.4.
  * Wednesday - Archive every Wednesday. Introduced in NLog 4.4.4.
  * Thursday - Archive every Thursday. Introduced in NLog 4.4.4.
  * Friday - Archive every Friday. Introduced in NLog 4.4.4.
  * Saturday - Archive every Saturday. Introduced in NLog 4.4.4.
> Files are moved to the archive as part of the write operation if the current period of time changes. For example if the current hour changes from 10 to 11, the first write that will occur on or after 11:00 will trigger the
> archiving. Caution: Enabling this option can considerably slow down your file logging in multi-process scenarios. If only one process is going to be writing to the file, consider setting ConcurrentWrites to false for maximum
> performance.

* **archiveDateFormat** - Specifies the date format used for archive numbering. Default format depends on the archive period. This option works only when the "ArchiveNumbering" parameter is set to Date or DateAndSequence

* **ArchiveOldFileOnStartup** - Achive old log file on startup.

### Output Options
* **replaceFileContentsOnEachWrite** - Indicates whether to replace file contents on each write instead of appending log message at the end. [Boolean](Data-types) Default: False  

* **fileAttributes** - File attributes (Windows only).  
Possible values:
  * Archive - File should be archived.
  * ~~Compressed~~ - Compress won't work due to .Net restrictions. You can use enableArchiveFileCompression.
  * DeleteOnClose - Delete file after it is closed.
  * Device - Device file.
  * Encrypted - Encrypted file.
  * Hidden - Hidden file.
  * NoBuffering - The system opens a file with no system caching.
  * Normal - Normal file.
  * NotContentIndexed - File should not be indexed by the content indexing service.
  * PosixSemantics - A file is accessed according to POSIX rules.
  * Readonly - Read-only
  * ReadOnly - Read-only file.
  * ReparsePoint - Reparse point.
  * SparseFile - Sparse file.
  * System - System file.
  * Temporary - File is temporary (should be kept in cache and not written to disk if possible).
  * WriteThrough - The system writes through any intermediate cache and goes directly to disk.
    > This parameter is not supported in:
    > * Silverlight 4.0

* **fileName** - Name of the file to write to. [Layout](Data-types) Required.  
This FileName string is a layout which may include instances of layout renderers. This lets you use a single target to write to multiple files.  
The following value makes NLog write logging events to files based on the log level in the directory where the application runs. `${basedir}/${level}.log` All Debug messages will go to `Debug.log`, all Info messages will go to `Info.log` and so on. You can combine as many of the layout renderers as you want to produce an arbitrary log file name. Since NLog 4.3 the `${basedir}` isn't needed anymore for relative paths.

* **deleteOldFileOnStartup** - Indicates whether to delete old log file on startup. [Boolean](Data-types) Default: False. This option works only when the "FileName" parameter denotes a single file.

* **enableFileDelete** - Indicates whether to enable log file(s) to be deleted. [Boolean](Data-types) Default: True  

* **createDirs** - Indicates whether to create directories if they don't exist. [Boolean](Data-types) Default: True  
Setting this to false may improve performance a bit, but you'll receive an error when attempting to write to a directory that's not present.

* **enableArchiveFileCompression** - Indicates whether to compress the archive files into the zip files. [Boolean](Data-types) Default: False
    > Supported in:
    > * NLog v4.0 for .NET 4.5

* **writeFooterOnArchivingOnly** - Indicates whether the footer should be written only when the file is archived. If `False`, the footer will also be written when starting to write to a different file and when the target is closed [Boolean](Data-types) Default: False

### Performance Tuning Options
* **keepFileOpen** - Indicates whether to keep log file open instead of opening and closing it on each logging event. Changing this property to true will improve performance a lot, but will also keep the file handle locked. Consider setting _openFileCacheTimeout_ = 30 when enabling this, as it will allow archive operations and react to log file being deleted. [Boolean](Data-types) Default: False 

* **concurrentWrites** - Enables support for optimized concurrent writes to same log file from multiple processes on the same machine-host, when using _keepFileOpen_ = true. By using a special technique that lets it keep the files open from multiple processes. If only single process (and single AppDomain) application is logging, then it is faster to set to _concurrentWrites_ = False.  [Boolean](Data-types) Default: True

* **openFileCacheTimeout** - Maximum number of seconds that files are kept open. If this number is negative the files are not automatically closed after a period of inactivity. [Integer](Data-types#integer) Default: -1  

* **openFileCacheSize** - Number of files to be kept open. Setting this to a higher value may improve performance in a situation where a single File target is writing to many files (such as splitting by level or by logger). [Integer](Data-types#integer) Default: 5  
The files are managed on a LRU (least recently used) basis, which flushes the files that have not been used for the longest period of time should the cache become full. As a rule of thumb, you shouldn't set this parameter to a very high value. A number like 10-15 shouldn't be exceeded, because you'd be keeping a large number of files open which consumes system resources.

* **optimizeBufferReuse** - Instead of allocating new buffers for every file write and for each layout rendering of log message, then it reuse the same buffers. [Boolean](Data-types) Default: True. Introduced in NLog 4.4.2

* **networkWrites** - Indicates whether concurrent writes to the log file by multiple processes on different network hosts. [Boolean](Data-types) Default: False  
This effectively prevents files from being kept open.

* **concurrentWriteAttemptDelay** - Delay in milliseconds to wait before attempting to write to the file again. [Integer](Data-types#integer) Default: 1  
The actual delay is a random value between 0 and the value specified in this parameter. On each failed attempt the delay base is doubled up to ConcurrentWriteAttempts times.  
Assuming that ConcurrentWriteAttemptDelay is 10 the time to wait will be: a random value between 0 and 10 milliseconds - 1st attempt a random value between 0 and 20 milliseconds - 2nd attempt a random value between 0 and 40 milliseconds - 3rd attempt a random value between 0 and 80 milliseconds - 4th attempt ... and so on.

* **concurrentWriteAttempts** - Number of times the write is attempted on the file before NLog discards the log message. [Integer](Data-types#integer) Default: 10  

* **cleanupFileName** - before writing to a file, the name of the file get checked for illegal characters (OS dependent). This can be costly if a lot of messages are written. The cleanup is cached for fixed names (no layout renderers). Set this to `false` for optimal performance (but beware of the file name, if it's wrong, nothing gets written). Default: `true`. Introduced in NLog 4.2.3.

* **bufferSize** - Log file buffer size in bytes. [Integer](Data-types#integer) Default: 32768  

* **autoFlush** - Indicates whether to automatically flush the file buffers after each log message. Disabling this will improve performance (See also **openFileFlushTimeout**).  [Boolean](Data-types) Default: True  

* **openFileFlushTimeout** - Number of seconds between explicit flush of file buffers. Helps to ensure file buffers are eventually flushed when **autoFlush = false**. [Integer](Data-types#integer) Default: 0
    > Introduced with NLog v4.5.7

## Examples
### Simple logging
The simplest use of File target is to produce single log file. In order to do this, put the following code in the configuration file such as NLog.config. Logs wil be written to logfile.txt in logs directory.
```xml
<?xml version="1.0" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 
    <targets>
        <target name="file" xsi:type="File"
            layout="${longdate} ${logger} ${message}${exception:format=ToString}" 
            fileName="${basedir}/logs/logfile.txt" 
            keepFileOpen="true"
            encoding="utf-8" />
    </targets>
 
    <rules>
        <logger name="*" minlevel="Debug" writeTo="file" />
    </rules>
</nlog>
```

### Archive old log files
NLog 4.5 makes it easy to setup archive logic to move/cleanup old files. You just need to configure `maxArchiveFiles` and it will automatically perform cleanup.

If the `fileName` is static and doesn't include a `${date}` layout, then you can use `archiveEvery="Day"` to ensure that it starts a new logfile every day. If the `fileName` does include `${date}` layout, then you should NOT configure `archiveEvery` (Unless it is `Year` for very special cases).

If the logfile becomes very large and slow to view, then you can use `archiveAboveSize=` to ensure that it starts a new logfile when filesize reaches a certain limit.

```xml
<?xml version="1.0" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 
    <targets>
        <target name="file" xsi:type="File"
            layout="${longdate} ${logger} ${message}${exception:format=ToString}" 
            fileName="${basedir}/logs/logfile.txt" 
            maxArchiveFiles="4"
            archiveAboveSize="10240"
            archiveEvery="Day" />
    </targets>
 
    <rules>
        <logger name="*" minlevel="Debug" writeTo="file" />
    </rules>
</nlog>
```

It will generate the following filenames:
```
* logfile.txt
* logfile.3.txt
* logfile.2.txt
* logfile.1.txt
```

If using NLog older than ver. 4.5 (or have very special needs), then also see [[FileTarget-Archive-Examples]]


### Per-level log files
Single File target can be used to write to multiple files at once. The following configuration will cause log entries for each log level to be written to a separate file, so you will get:
 * Trace.log
 * Debug.log
 * Info.log
 * Warn.log
 * Error.log
 * Fatal.log

```xml
<?xml version="1.0" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 
    <targets>
        <target name="file" xsi:type="File"
            layout="${longdate} ${logger} ${message}${exception:format=ToString}" 
            fileName="${basedir}/${level}.log" />
    </targets>
 
    <rules>
        <logger name="*" minlevel="Debug" writeTo="file" />
    </rules>
</nlog>
```
### One log file per day
The following configuration will create one log file for each day. Log files will be named:
 * 2010-06-05.log
 * 2010-06-06.log
 * 2010-06-07.log
 * 2010-06-08.log
 * ...
```xml
<?xml version="1.0" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 
    <targets>
        <target name="file" xsi:type="File"
            layout="${longdate} ${logger} ${message}${exception:format=ToString}" 
            fileName="${basedir}/${shortdate}.log" />
    </targets>
 
    <rules>
        <logger name="*" minlevel="Debug" writeTo="file" />
    </rules>
</nlog>
```

### Asynchronous logging
Depending on your usage scenario it may be useful to add an AsyncWrapper target the file target. This way all your log messages will be written on a separate thread so your main thread can be unblocked more quickly. Asynchronous logging is recommended for multi-threaded server applications which run for a long time and is not recommended for quickly-finishing command line applications.
```xml
<?xml version="1.0" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 
    <targets>
        <!-- Log in a separate thread, possibly queuing up to
        5000 messages. When the queue overflows, discard any
        extra messages-->
 
        <target name="file" xsi:type="AsyncWrapper" queueLimit="5000" overflowAction="Discard">
            <target xsi:type="File" fileName="${basedir}/logs/${level}.txt" keepFileOpen="true" />
        </target>
    </targets>
 
    <rules>
        <logger name="*" minlevel="Debug" writeTo="file" />
    </rules>
</nlog>
```
### Creating comma-separated log file (CSV)
In order to create comma-separated files (CSV), use the following configuration, which utilizes CsvLayout. The resulting file will have 4 columns and will be formatted according to CSV rules:
```xml
<?xml version="1.0" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <targets>
        <target name="csv" xsi:type="File" fileName="${basedir}/file.csv">
            <layout xsi:type="CSVLayout">
                <column name="time" layout="${longdate}" />
                <column name="message" layout="${message}" />
                <column name="logger" layout="${logger}"/>
                <column name="level" layout="${level}"/>
            </layout>
        </target>
    </targets>
 
    <rules>
        <logger name="*" minlevel="Debug" writeTo="csv" />
    </rules>
</nlog>
```