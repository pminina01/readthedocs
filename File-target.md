Writes log messages to one or more files. 

Since NLog 4.3 the `${basedir}` isn't needed anymore for relative paths.

Supported in .NET, Silverlight, Compact Framework and Mono.
##Configuration Syntax
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
          writeFooterOnArchivingOnly="Boolean"  />
</targets>
```
Read more about using the [Configuration File](Configuration-file).
##Parameters
###General Options
_name_ - Name of the target.

_forceManaged_ - Indicates that the file target should only use managed methods. This disables some of the options.
###Layout Options
_layout_ - Text to be rendered. [Layout](Layouts) Required. Default: `${longdate}|${level:uppercase=true}|${logger}|${message}`

_header_ - Header. [Layout](Layouts)  

_footer_ - Footer. [Layout](Layouts)

_encoding_ - File encoding name like "utf-8", "ascii" or "utf-16". See [Encoding class on MSDN](http://msdn.microsoft.com/en-us/library/system.text.encoding%28v=vs.110%29.aspx). Defaults to `Encoding.Default` (`UTF-8` on silverlight)

_lineEnding_ - Line ending mode.  
Possible values:
  * CR - Insert CR character (ASCII 13) after each line.
  * CRLF - Insert CR LF sequence (ASCII 13, ASCII 10) after each line.
  * Default - Insert platform-dependent end-of-line sequence after each line.
  * LF - Insert LF character (ASCII 10) after each line.
  * None - Don't insert any line ending.

###Archival Options
_archiveAboveSize_ - Size in bytes above which log files will be automatically archived. [Long](Layouts)  
Caution: Enabling this option can considerably slow down your file logging in multi-process scenarios. If only one process is going to be writing to the file, consider setting ConcurrentWrites to false for maximum performance. 
**Warning: combining this mode with _Archive Numbering Date_ is not supported. Archive files are not merged.    _ DateAndSequence_ do will work. **
 

_maxArchiveFiles_ - Maximum number of archive files that should be kept. If maxArchiveFiles is less or equal to 0, old files aren't deleted [Integer](Layouts) Default: 0  

_archiveFileName_ - Name of the file to be used for an archive. [Layout](Layouts)  
It may contain a special placeholder {#####} that will be replaced with a sequence of numbers depending on the archiving strategy. The number of hash characters used determines the number of numerical digits to be used for numbering files.  

_archiveNumbering_ - Way file archives are numbered.  
Possible values:
  * Rolling - Rolling style numbering (the most recent is always #0 then #1, ..., #N).
  * Sequence - Sequence style numbering. The most recent archive has the highest number.
  * Date - Date style numbering. The date is formatted according to the value of _archiveDateFormat_. **Warning: combining this mode with _archiveAboveSize_ is not supported. Archive files are not merged.  **
  * DateAndSequence - Combination of _Date_ and _Sequence_ .Archives will be stamped with the prior period (Year, Month, Day) datetime.
     The most recent archive has the highest number (in combination with the date). The date is formatted according to the value of _archiveDateFormat_.

See [Archive Numbering Examples](#archive-numbering-examples)

_archiveEvery_ - Indicates whether to automatically archive log files every time the specified time passes.  
Possible values:
  * Day - Archive daily.
  * Hour - Archive every hour.
  * Minute - Archive every minute.
  * Month - Archive every month.
  * None - Don't archive based on time.
  * Year - Archive every year.

Files are moved to the archive as part of the write operation if the current period of time changes. For example if the current hour changes from 10 to 11, the first write that will occur on or after 11:00 will trigger the archiving. Caution: Enabling this option can considerably slow down your file logging in multi-process scenarios. If only one process is going to be writing to the file, consider setting ConcurrentWrites to false for maximum performance.

_archiveDateFormat_ - Specifies the date format used for archive numbering. Default format depends on the archive period.

This option works only when the "ArchiveNumbering" parameter is set to Date or DateAndSequence

_ArchiveOldFileOnStartup_

aAchive old log file on startup.
###Output Options
_replaceFileContentsOnEachWrite_ - Indicates whether to replace file contents on each write instead of appending log message at the end. [Boolean](Data-types) Default: False  

_fileAttributes_ - File attributes (Windows only).  
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

_fileName_ - Name of the file to write to. [Layout](Data-types) Required.  
This FileName string is a layout which may include instances of layout renderers. This lets you use a single target to write to multiple files.  
The following value makes NLog write logging events to files based on the log level in the directory where the application runs. `${basedir}/${level}.log` All Debug messages will go to `Debug.log`, all Info messages will go to `Info.log` and so on. You can combine as many of the layout renderers as you want to produce an arbitrary log file name. Since NLog 4.3 the `${basedir}` isn't needed anymore for relative paths.

_deleteOldFileOnStartup_ - Indicates whether to delete old log file on startup. [Boolean](Data-types) Default: False  
This option works only when the "FileName" parameter denotes a single file.

_enableFileDelete_ - Indicates whether to enable log file(s) to be deleted. [Boolean](Data-types) Default: True  

_createDirs_ - Indicates whether to create directories if they don't exist. [Boolean](Data-types) Default: True  
Setting this to false may improve performance a bit, but you'll receive an error when attempting to write to a directory that's not present.

_enableArchiveFileCompression_ - Indicates whether to compress the archive files into the zip files. [Boolean](Data-types) Default: False
    > Supported in:
    > * NLog v4.0 for .NET 4.5

_writeFooterOnArchivingOnly_ - Indicates whether the footer should be written only when the file is archived. If `False`, the footer will also be written when starting to write to a different file and when the target is closed [Boolean](Data-types) Default: False

###Performance Tuning Options
_concurrentWrites_ - Indicates whether concurrent writes to the log file by multiple processes on the same host. [Boolean](Data-types) Default: True  
This makes multi-process logging possible. NLog uses a special technique that lets it keep the files open for writing.<br />**NOTE:** are ignored unless _keepFileOpen_ are set to true.

_openFileCacheTimeout_ - Maximum number of seconds that files are kept open. If this number is negative the files are not automatically closed after a period of inactivity. [Integer](Data-types) Default: -1  

_openFileCacheSize_ - Number of files to be kept open. Setting this to a higher value may improve performance in a situation where a single File target is writing to many files (such as splitting by level or by logger). [Integer](Data-types) Default: 5  
The files are managed on a LRU (least recently used) basis, which flushes the files that have not been used for the longest period of time should the cache become full. As a rule of thumb, you shouldn't set this parameter to a very high value. A number like 10-15 shouldn't be exceeded, because you'd be keeping a large number of files open which consumes system resources.

_networkWrites_ - Indicates whether concurrent writes to the log file by multiple processes on different network hosts. [Boolean](Data-types) Default: False  
This effectively prevents files from being kept open.

_concurrentWriteAttemptDelay_ - Delay in milliseconds to wait before attempting to write to the file again. [Integer](Data-types) Default: 1  
The actual delay is a random value between 0 and the value specified in this parameter. On each failed attempt the delay base is doubled up to ConcurrentWriteAttempts times.  
Assuming that ConcurrentWriteAttemptDelay is 10 the time to wait will be: a random value between 0 and 10 milliseconds - 1st attempt a random value between 0 and 20 milliseconds - 2nd attempt a random value between 0 and 40 milliseconds - 3rd attempt a random value between 0 and 80 milliseconds - 4th attempt ... and so on.

_concurrentWriteAttempts_ - Number of times the write is appended on the file before NLog discards the log message. [Integer](Data-types) Default: 10  

_cleanupFileName_ - before writing to a file, the name of the file get checked for illegal characters (OS dependent). This can be costly if a lot of messages are written. The cleanup is cached for fixed names (no layout renderers). Set this to `false` for optimal performance (but beware of the file name, if it's wrong, nothing gets written). Default: `true`. Introduced in NLog 4.2.3.

_bufferSize_ - Log file buffer size in bytes. [Integer](Data-types) Default: 32768  

_autoFlush_ - Indicates whether to automatically flush the file buffers after each log message. [Boolean](Data-types) Default: True  

_keepFileOpen_ - Indicates whether to keep log file open instead of opening and closing it on each logging event. [Boolean](Data-types) Default: False  
Setting this property to True helps improve performance.
##Examples
###Simple logging
The simplest use of File target is to produce single log file. In order to do this, put the following code in the configuration file such as NLog.config. Logs wil be written to logfile.txt in logs directory.
```xml
<?xml version="1.0" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 
    <targets>
        <target name="file" xsi:type="File"
            layout="${longdate} ${logger} ${message}" 
            fileName="${basedir}/logs/logfile.txt" 
            keepFileOpen="false"
            encoding="iso-8859-2" />
    </targets>
 
    <rules>
        <logger name="*" minlevel="Debug" writeTo="file" />
    </rules>
</nlog>
```
###Per-level log files
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
            layout="${longdate} ${logger} ${message}" 
            fileName="${basedir}/${level}.log" />
    </targets>
 
    <rules>
        <logger name="*" minlevel="Debug" writeTo="file" />
    </rules>
</nlog>
```
###One log file per day
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
            layout="${longdate} ${logger} ${message}" 
            fileName="${basedir}/${shortdate}.log" />
    </targets>
 
    <rules>
        <logger name="*" minlevel="Debug" writeTo="file" />
    </rules>
</nlog>
```

###Asynchronous logging
Depending on your usage scenario it may be useful to add an AsyncWrapper target the file target. This way all your log messages will be written on a separate thread so your main thread can be unblocked more quickly. Asynchronous logging is recommended for multi-threaded server applications which run for a long time and is not recommended for quickly-finishing command line applications.
```xml
<?xml version="1.0" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 
    <targets>
        <!-- Log in a separate thread, possibly queueing up to
        5000 messages. When the queue overflows, discard any
        extra messages-->
 
        <target name="file" xsi:type="AsyncWrapper" queueLimit="5000" overflowAction="Discard">
            <target xsi:type="File" fileName="${basedir}/logs/${level}.txt" />
        </target>
    </targets>
 
    <rules>
        <logger name="*" minlevel="Debug" writeTo="file" />
    </rules>
</nlog>
```
###Creating comma-separated log file (CSV)
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
###Size-based file archival
Log files can be automatically archived by moving them to another location after reaching certain size. The following configuration will create logs/logfile.txt which will be archived to archives/log.000000.txt', archives/log.000001.txt', archives/log.000002.txt' and so on once the main log file reaches 10KB.
```xml
<?xml version="1.0" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 
    <targets>
        <target name="file" xsi:type="File"
            layout="${longdate} ${logger} ${message}" 
            fileName="${basedir}/logs/logfile.txt" 
            archiveFileName="${basedir}/archives/log.{#####}.txt"
            archiveAboveSize="10240"
            archiveNumbering="Sequence"
            concurrentWrites="true"
            keepFileOpen="false"
            encoding="iso-8859-2" />
    </targets>
 
    <rules>
        <logger name="*" minlevel="Debug" writeTo="file" />
    </rules>
</nlog>
```
###Time-based file archival
Log files can calso be automatically archived based on time. This configuration will archive a file at the beginning of each day and will use rolling file naming, so log file from the previous day can always be found in archives//log.0.txt, log from two days ago is in archives//log.1.txt and so on. This configuration will keep at most 7 archive files, so logs older than one week will be automatically deleted.
```xml
<?xml version="1.0" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 
    <targets>
        <target name="file" xsi:type="File"
            layout="${longdate} ${logger} ${message}" 
            fileName="${basedir}/logs/logfile.txt" 
            archiveFileName="${basedir}/archives/log.{#}.txt"
            archiveEvery="Day"
            archiveNumbering="Rolling"
            maxArchiveFiles="7"
            concurrentWrites="true"
            keepFileOpen="false"
            encoding="iso-8859-2" />
    </targets>
 
    <rules>
        <logger name="*" minlevel="Debug" writeTo="file" />
    </rules>
</nlog>
```


###Archive Numbering Examples

####Rolling
```xml
        <target name="file" xsi:type="File"
            ...
            archiveFileName="log.{####}.txt"
            archiveNumbering="Rolling"  />

```

Example archive file names:

* log.0000.txt
* log.0001.txt
* log.0002.txt

####Sequence
```xml
        <target name="file" xsi:type="File"
            ...
            archiveFileName="log.{####}.txt"
            archiveNumbering="Sequence"  />

```

Example archive file names:

* log.0000.txt
* log.0001.txt
* log.0002.txt

####Date
```xml
        <target name="file" xsi:type="File"
            ...
            archiveFileName="log.{#}.txt"
            archiveNumbering="Date"
            archiveEvery="Day"
            archiveDateFormat="yyyyMMdd"
  />

```

Example archive file names:

* log.20150730.txt
* log.20150731.txt


####DateAndSequence
```xml
        <target name="file" xsi:type="File"
            ...
            archiveFileName="log.{#}.txt"
            archiveNumbering="DateAndSequence"
            archiveAboveSize="1000"
            archiveDateFormat="yyyyMMdd"
  />

```

Example archive file names:

* log.20150730.1.txt
* log.20150730.2.txt
* log.20150730.3.txt
