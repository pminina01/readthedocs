NLog allows for a custom time source to be provided when timestamping log
entries. In addition, NLog provides a few default time sources that can easily
be configured via XML or code.

By default, NLog uses the `FastLocal` as the default time source.

Note that the time source is used mostly for accuracy, so there might be some
quirks if using different time zones.

The following sections were based and/or provided by [Robert Važan’s
blog](<http://blog.angeloflogic.com/>):

-   [NLog timestamps with millisecond
    accuracy](<http://blog.angeloflogic.com/2013/10/nlog-timestamps-with-millisecond.html>)

-   [How to configure NLog time
    source](<http://blog.angeloflogic.com/2013/10/how-to-configure-nlog-time-source.html>)

-   [How to write custom NLog time
    source](<http://blog.angeloflogic.com/2013/10/how-to-write-custom-nlog-time-source.html>)

### Configure Via XML

The time source can be configured via XML by setting the time element with the
XML name. The provided time sources don’t include “TimeSource” in their XML
names.

```xml
<nlog>
    <time type="FastLocal" />
    <!-- Rest of Configuration -->
</nlog>
```

### Configure Via Runtime Configuration

The time source can be configured by inserting the following before any log
messages are printed:

```csharp
TimeSource.Current = new FastLocalTimeSource();
```

### Provided Time Sources

The provided time sources range from accurate to fast with options for a Local
or UTC time.

The accuracy relates directly to Windows and how it balances accuracy, speed,
and efficiency (i.e. battery life). By default, Windows is set to 16ms of
accuracy, but can be changed via the API calls of
[timeBeginPeriod](https://msdn.microsoft.com/en-us/library/dd757624)
and
[timeEndPeriod](https://msdn.microsoft.com/en-us/library/dd757626).
The `AccurateLocal` and `AccurateUTC` both utilize this API to provide a more
accurate time reading.

The speed of UTC is faster than the local variant, as the time zone conversion can take some time.

Below are the provided time sources with NLog:

| **XML Configuration** | **Is Default?** | **Runtime Configuration** | **Time** | **Accuracy** | **Speed** |
|-----------------------|-----------------|---------------------------|----------|--------------|-----------|
| FastLocal             | Yes             | FastLocalTimeSource       | local    | 16ms         | very fast |
| FastUTC               | No              | FastUtcTimeSource         | UTC      | 16ms         | fastest   |
| AccurateLocal         | No              | AccurateLocalTimeSource   | local    | 1ms          | slow      |
| AccurateUTC           | No              | AccurateUtcTimeSource     | UTC      | 1ms          | fast      |

Performance benchmarks for time source implementations (used [BenchmarkDotNet](https://github.com/PerfDotNet/BenchmarkDotNet)):

|        Method |      Median |     StdDev |
|-------------- |-----------: |----------: |
|     FastLocal |   5.7752 ns |  0.3450 ns |
|       FastUtc |   5.8330 ns |  0.4939 ns |
| AccurateLocal | 784.4354 ns | 61.6136 ns |
|   AccurateUtc |   7.0547 ns |  0.3934 ns |

### Custom Time Source

Before implementing your own time source, see the provided time sources first.
If none of those fit your needs, this section will guide you through the
process.

Create a class that inherits from TimeSource and implement the inherited
property getter `Time` and method `FromSystemTime`.

-   The property getter `Time` provides the current time instance.

-   The method FromSystemTime converts the system time to the same form as if
    the time source provided it.

```csharp
[TimeSource("CustomTimeZone")]
public class CustomTimeZoneTimeSource : TimeSource
{
    string ZoneName;
    TimeZoneInfo ZoneInfo;

    [Required]
    public string Zone
    {
        get { return ZoneName; }
        set
        {
            ZoneName = value;
            ZoneInfo
                = TimeZoneInfo.FindSystemTimeZoneById(value);
        }
    }
    
    public override DateTime Time
    {
        get
        {
            return TimeZoneInfo.ConvertTimeFromUtc(
                DateTime.UtcNow, ZoneInfo);
        }
    }
    
    public override DateTime FromSystemTime(DateTime systemTime)
    {
        return TimeZoneInfo.ConvertTimeFromUtc(systemTime, ZoneInfo);
    }
}
```

In addition, add an attribute to the top that provides the name when specifying
the type via XML.

Your custom time source can be loaded by NLog just like any other NLog
extension. See [how to use the custom target / layout
renderer](<Extending%20NLog>).

The Runtime Configuration would look like this:

```csharp
TimeSource.Current = new CustomTimeZoneTimeSource()
{
    Zone = "Central Standard Time"
}
```

The XML Configuration would look like this:

```xml
<nlog>
    <time type="CustomTimeZone" zone="Central Standard Time" />
</nlog>
```