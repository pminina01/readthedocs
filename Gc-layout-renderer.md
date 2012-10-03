The information about the garbage collector. 

Supported in .NET and Silverlight

##Configuration Syntax
```
${gc:property=Enum}
```

##Parameters
###Rendering Options
* **property** - Property to retrieve. Default: TotalMemory  
  Possible values:
  * CollectionCount0 - The number of Gen0 collections.
  * CollectionCount1 - The number of Gen1 collections.
  * CollectionCount2 - The number of Gen2 collections.
  * MaxGeneration - Maximum generation number supported by GC.
  * TotalMemory - Total memory allocated.
  * TotalMemoryForceCollection - Total memory allocated (perform full garbage collection first)