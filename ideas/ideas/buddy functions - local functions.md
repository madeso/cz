---
title: Buddy functions
summary: A local function declared outside the main body
tags:
    - for-functions
---

Buddy (or body) functions / local functions are:

- Functions inside a function
- Not exposed outside the container function
- Defined after the container function

```c
fun foo()
{
    bar();
}
#fun bar()
{
    // ...
}
```

## Why?
To reduce indenting with 1 step for local functions...

### Design issue
Can a buddy function call another buddy function? How much do we gain with this compared to just not exposing a function outside the current "module".