---
title: "State hints"
summary: "Instead of custom logic for certain types, have editor types instead"
tags:
    - editor
    - for-types
---

```c
// sample optional implementation with kotlin like editor hints
struct Optional<T>
{
    union struct {
        None: {}, Value {value: T}
    } data;
    // union of typesafe anonomous structs

    #imply_var {has: bool => .data == .Value;}
    // there is a variable, when it is true .data has to have a value

    fun has_value(): bool
    #imply_result(return == true => has==true)
    // if the return value is true, the has property has to be true
    {
        return data == .Value;
    }

    fun get(): T
    #imply_require(has == true)
    // this function can only be called if has is true
    {
        // if has is true, the declartion of has implies that data is Value and we can access value safely
        return data.value;
    }
};
```