Log text a Rich Text Box control in an existing or new form. 

Supported in .NET
##Configuration Syntax
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
Read more about using the [Configuration File](Configuration-file).
##Parameters
#¤#General Options
_name_ - Name of the target.
###Layout Options
_layout_ - Layout used to format log messages. Required. Default: ${longdate}|${level:uppercase=true}|${logger}|${message}
###Form Options
_height_ - Initial height of the form with rich text box.  
This parameter is ignored when logging to existing form control.   
> This parameter is not supported in:
> * NLog v1.0 for .NET Framework 1.0
> * NLog v1.0 for .NET Framework 1.1
> * NLog v1.0 for .NET Framework 2.0

_autoScroll_ - Indicates whether scroll bar will be moved automatically to show most recent log entries.  
> This parameter is not supported in:
> * NLog v1.0 for .NET Framework 1.0
> * NLog v1.0 for .NET Framework 1.1
> * NLog v1.0 for .NET Framework 2.0

_maxLines_ - Maximum number of lines the rich text box will store (or 0 to disable this feature).  
After exceeding the maximum number, first line will be deleted.  
> This parameter is not supported in:
> * NLog v1.0 for .NET Framework 1.0
> * NLog v1.0 for .NET Framework 1.1
> * NLog v1.0 for .NET Framework 2.0

_showMinimized_ - Indicates whether the created form will be initially minimized.  
This parameter is ignored when logging to existing form control.  
> This parameter is not supported in:
> * NLog v1.0 for .NET Framework 1.0
> * NLog v1.0 for .NET Framework 1.1
> * NLog v1.0 for .NET Framework 2.0

_toolWindow_ - Indicates whether the created window will be a tool window. Default: True  
This parameter is ignored when logging to existing form control. Tool windows have thin border, and do not show up in the task bar.  
> This parameter is not supported in:
> * NLog v1.0 for .NET Framework 1.0
> * NLog v1.0 for .NET Framework 1.1
> * NLog v1.0 for .NET Framework 2.0

_controlName_ - Name of RichTextBox to which Nlog will write.

_formName_ - Name of the Form on which the control is located. If there is no open form of a specified name then NLog will create a new one.

_width_ - Initial width of the form with rich text box.  
This parameter is ignored when logging to existing form control.  
> This parameter is not supported in:
> * NLog v1.0 for .NET Framework 1.0
> * NLog v1.0 for .NET Framework 1.1
> * NLog v1.0 for .NET Framework 2.0

###Highlighting Options
_wordColoringRules_ - The word highlighting rules. Collection  
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

_text_ - Text to be matched. You must specify either text or regex.

_wholeWords_ - Indicates whether to match whole words only. Boolean Default: False

_useDefaultRowColoringRules_ - Indicates whether to use default cooring rules.Boolean Default: False

_rowColoringRules_ - The row coloring rules. Collection  
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