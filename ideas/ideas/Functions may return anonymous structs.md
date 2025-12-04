---
title: 'Functions may return anonymous structs'
summary: ' '
tags:
    - for-functions
---

```c
fun foo(): struct {int x;}
{
    return {x: 42};
}
```

Why? Some functions have a specific set of return variables and perhaps it's prefered to not have tuple, but also not need to name this structure due to the return value of `foo` being `FooReturn` would just be clutter.