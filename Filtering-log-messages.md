Log messages may be filtered via either _routing_ or _filtering_.

## Filters

With the use of `<filters>` you may ignore (blacklist) and/or allow (whitelist) events. See the [`<when>` filter](When-filter).

e.g.
```xml
<logger name="*" writeTo="file">
   <filters>
    <when condition="length('${message}') > 100" action="Ignore" />
  </filters>
</logger> 
```

## Routing

Log messages may be filtered by logger name. Write the messages to a `Null` target and use `final="true"`.

```xml
<targets>
  <target xsi:type="Null" name="BlackHole" formatMessage="false"  />
</targets>
<rules>
   <!-- ignore events written that are written to a logger which starts with "Namespace." -->
   <logger name="Namespace.*" minlevel="Debug" writeTo="BlackHole" final="true" />     
</rules>
```

Compared to the `<filters>` this is more efficient and could be easier to write. 

### Deprecated filters

These filters are deprecated. They have been replace by the `<when>` filter, which exposes uses modifiable conditions for filtering log events.

* [`<whenContains>` filter](WhenContains-filter) - Matches when the calculated layout contains the specified substring. 
* [`<whenEqual>` filter](WhenEqual-filter) - Matches when the calculated layout is equal to the specified substring. 
* [`<whenNotContains>` filter](WhenNotContains-filter) - Matches when the calculated layout does NOT contain the specified substring. 
* [`<whenNotEqual>` filter](WhenNotEqual-filter) - Matches when the calculated layout is NOT equal to the specified substring. 