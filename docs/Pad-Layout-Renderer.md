Applies padding to another layout output. 

Supported in .NET, Silverlight, Compact Framework and Mono.

## Configuration Syntax
```
${pad:padCharacter=Char:padding=Integer:fixedLength=Boolean
     :inner=Layout:alignmentOnTruncation=PaddingHorizontalAlignment}
```

or by using ambient property to modify output of other layout renderer:

```
${other:padCharacter=Char}
```

## Parameters
### Transformation Options
* **padCharacter** - Padding character. `Char` Default: (space character)
* **padding** - Number of characters to pad the output to.
Positive padding values cause left padding, negative values cause right padding to the desired width. `Integer`
* **fixedLength** - Indicates whether to trim the rendered text to the absolute value of the padding length. `Boolean` Default: `False`
* **inner** - Wrapped layout. `Layout`
* **alignmentOnTruncation** - Indicates whether a value that has been truncated due to `fixedLength=true` is aligned to the `left` (characters removed from the right) or `right` (characters removed from the left). This is independent of the alignment applied when padding shorter strings out to `padding` characters. This property was introduced in NLog 4.0. Earlier versions always apply an alignment equivalent to `alignmentOnTruncation=left`. `PaddingHorizontalAlignment` Default: `Left`