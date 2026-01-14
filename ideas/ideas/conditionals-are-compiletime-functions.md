---
title: "Conditionals as compiletime functions"
summary: "Instead of if, call a function"
tags:
    - questionable
    - dsl
    - for-functions
---

## Possible syntax
A compile time function called `if` is called. If there is a body is after the function call, the body is appended to the argument list.
```cpp
if(condition) {
    // ...
}
```

If multiple bodies needs to be supplied, we can use named arguments:
```cpp
if(condition)
    then: {
        // ...
    }
    else: {
        // ...
    }
```

Body arguments can also take a extra argument
```cpp
switch(var)
    case(a): {
        // ...
    }
    case(b): {
        // ...
    }
```

### See also
* {{<link "custom-frontend.md">}}
