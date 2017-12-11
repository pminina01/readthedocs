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

* **concurrentWriteAttempts** - Number of times the write is appended on the file before NLog discards the log message. [Integer](Data-types#integer) Default: 10  

* **cleanupFileName** - before writing to a file, the name of the file get checked for illegal characters (OS dependent). This can be costly if a lot of messages are written. The cleanup is cached for fixed names (no layout renderers). Set this to `false` for optimal performance (but beware of the file name, if it's wrong, nothing gets written). Default: `true`. Introduced in NLog 4.2.3.

* **bufferSize** - Log file buffer size in bytes. [Integer](Data-types#integer) Default: 32768  

* **autoFlush** - Indicates whether to automatically flush the file buffers after each log message. [Boolean](Data-types) Default: True  

## Examples
### Simple logging
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
            layout="${longdate} ${logger} ${message}" 
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
            layout="${longdate} ${logger} ${message}" 
            fileName="${basedir}/${shortdate}.log" />
    </targets>
 
    <rules>
        <logger name="*" minlevel="Debug" writeTo="file" />
    </rules>
</nlog>
```


### One log file per application instance, remove old logs
The following configuration will create a dedicated log file for each start of your application. Multiple instances can run in parallel and write to their respective log file. By adding a timestamp to the filename, each filename is unique (up to the second). Up to ten log files (active + nine archive) are kept. The removal of old logs works, when the `archiveFileName` contains a placeholder, `archiveDateFormat` has the same datetime format as in the `name` property, and `archiveNumbering` and `archiveEvery` are enabled. The `$(cached:...)` directive prevents that a new log file name is generated for every log entry. Log files will be named:
 * 2017-11-05 08_00_00.log
 * 2017-11-05 08_00_01.log
 * 2017-11-05 12_35_04.log
 * 2017-11-06 09_54_32.log
 * ...
```xml
<?xml version="1.0" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

     <targets>
        <target name="file" xsi:type="File"
            layout="${longdate} ${logger} ${message}" 
            fileName="${basedir}/${cached:${date:format=yyyy-MM-dd HH_mm_ss}}.log"
            archiveFileName="${basedir}/{#}.log"
            archiveDateFormat="yyyy-MM-dd HH_mm_ss"
            archiveNumbering="Date"
            archiveEvery="Year"
            maxArchiveFiles="9" />
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
### Size-based file archival
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
### Time-based file archival
Log files can also be automatically archived based on time. This configuration will archive a file at the beginning of each day and will use rolling file naming, so log file from the previous day can always be found in archives//log.0.txt, log from two days ago is in archives//log.1.txt and so on. This configuration will keep at most 7 archive files, so logs older than one week will be automatically deleted.
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


#### Archive every Week
You can specify different archival time periods. For example, if you wanted to archive once a week on Tuesdays,
you would set `archiveEvery="Tuesday"`. Possible values for `archiveEvery` can be found above. This will result in
the following files being created:
+ logfile.txt           // the current log being written to
+ logfile.20170307.txt
+ logfile.20170314.txt
+ logfile.20170321.txt
+ etc.

```xml
<?xml version="1.0" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 
    <targets>
        <target name="file" xsi:type="File"
            layout="${longdate} ${logger} ${message}" 
            fileName="${basedir}/logs/logfile.txt" 
            archiveFileName="${basedir}/archives/logfile.{#}.txt"
            archiveEvery="Tuesday"
            maxArchiveFiles="7" />
    </targets>
 
    <rules>
        <logger name="*" minlevel="Debug" writeTo="file" />
    </rules>
</nlog>
```


### Archive Numbering Examples

#### Rolling
```xml
        <target name="file" xsi:type="File"
            ...
            fileName="file.txt"
            archiveFileName="log.{####}.txt"
            archiveNumbering="Rolling"  />

```

Example of file names (newest files first):

* file.txt
* log.0000.txt
* log.0001.txt
* log.0002.txt

#### Sequence
```xml
        <target name="file" xsi:type="File"
            ...
            fileName="file.txt"
            archiveFileName="log.{####}.txt"
            archiveNumbering="Sequence"  />

```

Example of file names (newest files first):

* file.txt
* log.0002.txt
* log.0001.txt
* log.0000.txt

#### Date
```xml
        <target name="file" xsi:type="File"
            ...
            fileName="file.txt"
            archiveFileName="log.{#}.txt"
            archiveNumbering="Date"
            archiveEvery="Day"
            archiveDateFormat="yyyyMMdd"
  />

```

Example of file names (newest files first):

* file.txt
* log.20150731.txt
* log.20150730.txt

#### DateAndSequence
```xml
        <target name="file" xsi:type="File"
            ...
            fileName="file.txt"
            archiveFileName="log.{#}.txt"
            archiveNumbering="DateAndSequence"
            archiveAboveSize="1000"
            archiveDateFormat="yyyyMMdd"
  />

```

Example of file names (newest files first):

* file.txt
* log.20150730.3.txt
* log.20150730.2.txt
* log.20150730.1.txt