---
title: 'Sections inside a function'
summary: 'Similar to local functions but with less typing'
---

Works like a function but not named and immidiatly "called"

```c
fun foo(x, y)
{
    var a := x+y;
    use (x, y) {
        // only use x and y, outer variables aren't touched (or read)
        // should modification be legel here? might be more readable to treat everything as const
        x += 3;
        y += x;
        const c = x + 1;
    }
    with (
        const b = x+y;
        const c = ...; // if name match
    );

    return b + a;
}
```

## Why?
Compared to a location function, the local variables comes first and the return values exposed from the function comes after the block. Both code and data follows the logical top to bottom flow.

## Design note
should we allow early returns?