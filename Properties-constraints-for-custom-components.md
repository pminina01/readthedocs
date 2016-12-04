Custom Targets, layout etc. could have properties. There are only limitations if you like to set them from the XML config.

The following types are supported

## Targets

- C# types: e.g. bool, char, decimal, double, float, int, uint, etc.
- Enums
- `Encoding`
- `CultureInfo`
- `Type`
- `LineEndingMode` 
- `Uri`
- NLog types: `Layout`, `SimpleLayout` & `ConditionExpression`
- Types which has an implicit conversion from `string`
- Types which are using `TypeDescriptor` from `string` (not Silverlight)
- 