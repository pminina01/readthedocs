Log event all context data. 

Introduced in NLog v4.0.

Supported in .NET, Silverlight and Mono.

##Configuration Syntax
```
${all-event-properties:format=String:separator=String}
```

##Parameters
###Rendering Options
* _format_ - How key/value pairs will be formatted. The placeholder used to define placement of the key is, "[key]", and the placeholder for value is, "[value]".
  * Default value: "[key]=[value]"
* _separator_ - The string that will be used to separate key/value pairs.
  * Default value: ", "