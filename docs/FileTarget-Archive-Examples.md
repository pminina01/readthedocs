NLog ver. 4.5 makes it very [easy to perform archive of old files](https://github.com/NLog/NLog/wiki/File-target#archive-old-log-files). 

But there are many [archival options](https://github.com/NLog/NLog/wiki/File-target#archival-options), which allows one to configure the archive logic even further. This can be needed if using NLog older than ver. 4.5.

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
            layout="${longdate} ${logger} ${message}${exception:format=ToString}" 
            fileName="${basedir}/logs/${cached:${date:format=yyyy-MM-dd HH_mm_ss}}.log"
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
