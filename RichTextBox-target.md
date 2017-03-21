Log text a Rich Text Box control in an existing or new form. 

Supported in .NET

## Configuration Syntax
```xml
<targets>
  <target xsi:type="RichTextBox"
          name="String"
          layout="Layout"
          height="Integer"
          autoScroll="Boolean"
          maxLines="Integer"
          showMinimized="Boolean"
          toolWindow="Boolean"
          controlName="String"
          formName="String"
          width="Integer"
          useDefaultRowColoringRules="Boolean">
    <word-coloring backgroundColor="String" fontColor="String" ignoreCase="Boolean"
                regex="String" style="Enum" text="String"
                wholeWords="Boolean"/><!-- repeated -->
    <row-coloring backgroundColor="String" condition="Condition" fontColor="String"
               style="Enum"/><!-- repeated -->
  </target>
</targets>
```
Read more about using the [[Configuration File]].

## Parameters
#¤# General Options
* **name** - Name of the target.

###Layout Options
* **layout** - Layout used to format log messages. Required. Default: ${longdate}|${level:uppercase=true}|${logger}|${message}

###Form Options
* **height** - Initial height of the form with rich text box.  
This parameter is ignored when logging to existing form control.   
> This parameter is not supported in:
> * NLog v1.0 for .NET Framework 1.0
> * NLog v1.0 for .NET Framework 1.1
> * NLog v1.0 for .NET Framework 2.0

* **autoScroll** - Indicates whether scroll bar will be moved automatically to show most recent log entries.  
> This parameter is not supported in:
> * NLog v1.0 for .NET Framework 1.0
> * NLog v1.0 for .NET Framework 1.1
> * NLog v1.0 for .NET Framework 2.0

* **maxLines** - Maximum number of lines the rich text box will store (or 0 to disable this feature).  
After exceeding the maximum number, first line will be deleted.  
> This parameter is not supported in:
> * NLog v1.0 for .NET Framework 1.0
> * NLog v1.0 for .NET Framework 1.1
> * NLog v1.0 for .NET Framework 2.0

* **showMinimized** - Indicates whether the created form will be initially minimized.  
This parameter is ignored when logging to existing form control.  
> This parameter is not supported in:
> * NLog v1.0 for .NET Framework 1.0
> * NLog v1.0 for .NET Framework 1.1
> * NLog v1.0 for .NET Framework 2.0

* **toolWindow** - Indicates whether the created window will be a tool window. Default: True  
This parameter is ignored when logging to existing form control. Tool windows have thin border, and do not show up in the task bar.  
> This parameter is not supported in:
> * NLog v1.0 for .NET Framework 1.0
> * NLog v1.0 for .NET Framework 1.1
> * NLog v1.0 for .NET Framework 2.0

* **controlName** - Name of RichTextBox to which Nlog will write.

* **formName** - Name of the Form on which the control is located. If there is no open form of a specified name then NLog will create a new one.

* **width** - Initial width of the form with rich text box.  
This parameter is ignored when logging to existing form control.  
> This parameter is not supported in:
> * NLog v1.0 for .NET Framework 1.0
> * NLog v1.0 for .NET Framework 1.1
> * NLog v1.0 for .NET Framework 2.0

### Highlighting Options
* **wordColoringRules** - The word highlighting rules. Collection  
Each collection item is represented by \<word-coloring /> element with the following attributes:  
  * _backgroundColor_ - Background color. Names are identical with KnownColor enum extended with Empty value which means that background color won't be changed. Default: Empty
  * _fontColor_ - Font color. Names are identical with KnownColor enum extended with Empty value which means that font color won't be changed. Default: Empty
  * _ignoreCase_ - Indicates whether to ignore case when comparing texts. Boolean Default: False
  * _regex_ - Regular expression to be matched. You must specify either text or regex.
  * _style_ - Font style of matched text. Possible values are the same as in FontStyle enum in System.Drawing.
    Possible values:
    * Bold -
    * Italic -
    * Regular -
    * Strikeout -
    * Underline -

* **text** - Text to be matched. You must specify either text or regex.

* **wholeWords** - Indicates whether to match whole words only. Boolean Default: False

* **useDefaultRowColoringRules** - Indicates whether to use default cooring rules.Boolean Default: False

* **rowColoringRules** - The row coloring rules. Collection  
Each collection item is represented by \<row-coloring /> element with the following attributes:  
  * _backgroundColor_ - Background color. Names are identical with KnownColor enum extended with Empty value which means that background color won't be changed. Default: Empty
  * _fontColor_ - Font color. Names are identical with KnownColor enum extended with Empty value which means that font color won't be changed. Default: Empty
  * _ignoreCase_ - Indicates whether to ignore case when comparing texts. Boolean Default: False
  * _regex_ - Regular expression to be matched. You must specify either text or regex.
  * _style_ - Font style of matched text. Possible values are the same as in FontStyle enum in System.Drawing.  
    Possible values:
    * Bold -
    * Italic -
    * Regular -
    * Strikeout -
    * Underline -
    Possible values are the same as in FontStyle enum in System.Drawing