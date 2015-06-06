A counter value (increases on each layout rendering). 

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
Starting in NLog v4.0 the sequence options have been changed from String to layout

```
${counter:increment=Integer:sequence=Layout:value=Integer}
``` 

The syntax for versions below NLog v4.0 is:

```
${counter:increment=Integer:sequence=String:value=Integer}
``` 

##Parameters
###Counter Options
* **increment** - Value to be added to the counter after each layout rendering. Integer Default: 1
* **sequence** - Name of the sequence. Different named sequences can have individual values.
* **value** - Initial value of the counter. Integer Default: 1