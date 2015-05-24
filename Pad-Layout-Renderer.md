Applies padding to another layout output. 

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${pad:padCharacter=Char:padding=Integer:fixedLength=Boolean
     :inner=Layout}
```

or by using ambient property to modify output of other layout renderer:

```
${other:padCharacter=Char}
```

##Parameters
###Transformation Options
* _padCharacter_ - Padding character. `Char` Default: (space character)
* _padding_ - Number of characters to pad the output to.
Positive padding values cause left padding, negative values cause right padding to the desired width. `Integer`
* _fixedLength_ - Indicates whether to trim the rendered text to the absolute value of the padding length. `Boolean` Default: `False`
* _inner_ - Wrapped layout. `Layout`
* _alignmentOnTruncation_ - Indicates whether a value that has been truncated due to `fixedLength=true` is aligned to the `left` (characters removed from the right) or `right` (characters removed from the left). This is independent of the alignment applied when padding shorter strings out to `padding` characters. This property was introduced in NLog 4.0. Earlier versions always apply an alignment equivalent to `alignmentOnTruncation=left`. `PaddingHorizontalAlignment` Default: `Left`