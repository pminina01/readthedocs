Layout renderers are template macros that are used in [Layouts](Layouts), e.g. `${message}`, `${level}` etc

NLog supports creating custom layout renderers. For more information, see: [Extending NLog](Extending-NLog)


## Layout Renderers

All layout renderers could be found here: http://nlog-project.org/config/?tab=layout-renderers

## Passing Custom Values to a Layout
Even though the layout renderers provide many pre-defined values, you may need to pass application specific values to your [Layouts](Layouts). You can pass your own values in code by adding custom properties to the event. You then retrieve the value using the [${event-properties}](Event-Context-Layout-Renderer) renderer. See the documentation for the [${event-properties}](Event-Context-Layout-Renderer) for an example.