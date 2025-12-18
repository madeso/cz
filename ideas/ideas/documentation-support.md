---
title: "Documentation support"
summary: " "
tags:
    - header
    - documentation
---
I don't really like writing documentation in special comments so it would be nice support for a feature that is aware of the syntax so a editor or tool could use it more easily.

### References

### C++(...) "javadoc" doxygen comments
```cpp
/**
 * A brief history of JavaDoc-style (C-style) comments.
 *
 * This is the typical JavaDoc-style C-style comment. It starts with two
 * asterisks.
 *
 * @param theory Even if there is only one possible unified theory. it is just a
 *               set of rules and equations.
 */
void cstyle( int theory );
```
https://www.doxygen.nl/manual/docblocks.html

### C# xmldoc
```csharp
/// <summary>
/// Example using para tags:
/// <para>This is the first paragraph.</para>
/// <para>This is the second paragraph with double spacing.</para>
/// </summary>
public void FormattingExample()
{
    // This method demonstrates paragraph and line break formatting
}
```
https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/xmldoc/recommended-tags

### Python docstring
```python
def kos_root():
    """Return the pathname of the KOS root directory."""
    global _kos_root
    if _kos_root: return _kos_root
    ...
```
https://peps.python.org/pep-0257/
