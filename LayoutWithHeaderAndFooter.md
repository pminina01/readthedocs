A specialized layout that supports header and footer. 

Supported in .NET, Silverlight, Compact Framework and Mono
##Configuration Syntax
```xml
<targets>
  <target>
    <layout xsi:type="LayoutWithHeaderAndFooter">
      <!-- Layout Options -->
      <layout xsi:type="layoutType">Layout</layout>
      <header xsi:type="layoutType">Layout</header>
      <footer xsi:type="layoutType">Layout</footer>

    </layout>
  </target>
</targets>
```
##Parameters
###Layout Options
_layout_ - Body layout (can be repeated multiple times). Layout

_header_ - Header layout. Layout

_footer_ - Footer layout. Layout