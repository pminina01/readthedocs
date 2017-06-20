System special folder path (includes My Documents, My Music, Program Files, Desktop, and more). 

Supported in .NET, Silverlight and Mono.

## Configuration Syntax
```
${specialfolder:dir=String:file=String:folder=Enum}
```

## Parameters
### Advanced Options
* **dir** - Name of the directory to be Path.Combine()'d with the directory name.
* **file* - Name of the file to be Path.Combine()'d with the directory name.

### Rendering Options
* **folder** - System special folder to use.  
  Possible values:
  * AdminTools -
  * ApplicationData -
  * CDBurning -
  * CommonAdminTools -
  * CommonApplicationData -
  * CommonDesktopDirectory -
  * CommonDocuments -
  * CommonMusic -
  * CommonOemLinks -
  * CommonPictures -
  * CommonProgramFiles -
  * CommonProgramFilesX86 -
  * CommonPrograms -
  * CommonStartMenu -
  * CommonStartup -
  * CommonTemplates -
  * CommonVideos -
  * Cookies -
  * Desktop -
  * DesktopDirectory -
  * Favorites -
  * Fonts -
  * History -
  * InternetCache -
  * LocalApplicationData -
  * LocalizedResources -
  * MyComputer -
  * MyDocuments -
  * MyMusic -
  * MyPictures -
  * MyVideos -
  * NetworkShortcuts -
  * Personal -
  * PrinterShortcuts -
  * ProgramFiles -
  * ProgramFilesX86 -
  * Programs -
  * Recent -
  * Resources -
  * SendTo -
  * StartMenu -
  * Startup -
  * System -
  * SystemX86 -
  * Templates -
  * UserProfile -
  * Windows -

  Full list of options is available at [MSDN](https://msdn.microsoft.com/en-us/library/system.environment.specialfolder(v=vs.110).aspx). The most common ones are:
  * ApplicationData - roaming application data for current user.
  * CommonApplicationData - application data for all users.
  * MyDocuments - My Documents
  * DesktopDirectory - Desktop directory
  * LocalApplicationData - non roaming application data
  * Personal - user profile directory
  * System - System directory

## Example

```
fileName="${specialfolder:folder=ApplicationData}/Program/file.txt"
```