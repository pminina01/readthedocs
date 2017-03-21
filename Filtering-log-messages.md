Log messages could be filtered by using the routing or filtering abilities of NLog.

## Filters
With the use of `<Filters>` you could ignore (blacklist) and/or allow (whitelist) events. See the [when filter](When-filter).

e.g.
```xml
<logger name="*" writeTo="file">
   <filters>
    <when condition="length('${message}') > 100" action="Ignore" />
  </filters>
</logger> 
```



## Routing
Log messages could be filtered on the logger name. Write the messages to a Null target and use final, e.g.

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
These filters is deprecated in favour of `<when />` which is based on conditions.

* [whenContains filter](WhenContains-filter) - Matches when the calculated layout contains the specified substring. 
* [whenEqual filter](WhenEqual-filter) - Matches when the calculated layout is equal to the specified substring. 
* [whenNotContains filter](WhenNotContains-filter) - Matches when the calculated layout does NOT contain the specified substring. 
* [whenNotEqual filter](WhenNotEqual-filter) - Matches when the calculated layout is NOT equal to the specified substring. 