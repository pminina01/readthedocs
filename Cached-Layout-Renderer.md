Applies caching to another layout output. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${cached:cached=Boolean:clearCache=ClearCacheOption:inner=Layout:cacheKey=Layout}
```

or by using ambient property to modify output of other layout renderer:

```
${other:cached=Boolean}
```

## Parameters

### Caching Options
* _cached_ - Indicates whether this CachedLayoutRendererWrapper is enabled. Boolean Default: True
* _clearCache_ - Introduced in NLog 4.2. Indicates when the cache is cleared. Possible options: `None, OnInit, Onclose`.  ClearCacheOption Default: `OnInit, OnClose`. 
* _cacheKey_ - the layout to be checked if the cache is still valid. For example, the current day. Default `null`. Introduced in NLog 4.3.9

### Transformation Options
* _inner_ - Wrapped layout. Layout


## Examples
* `${cached:cached=true:clearCache=OnInit,OnClose:inner=l}`: The value of `l` is cached and the cache will be cleared when the layout renderer is initialized or when it is closed. This is the same as `${cached:cached=true:inner=l}`.
* `${cached:cached=true:clearCache=None:inner=l}`: The value of `l` is cached and the cache will not be cleared.
* `filename="${cached:cached=true:Inner=${date:format=yyyy-MM-dd hh.mm.ss}:CacheKey=${shortdate}}.log"` -  Use the first logtime and day in the file name, only one file per day.

## Remarks
The value of the inner layout will be rendered only once and reused subsequently.