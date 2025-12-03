---
title: 'built in types'
summary: 'strings, dyn-arrays, optionals, dicts, iterators & tuples'
---

Why? Compiler and IDE can provide better hints.
A possible optimization is that 7/31/63 bit integegers that can be null can be stored within their parent type, without needing additional storage needed. Cleaner syntax when there is only a vector and dictonary.

Counterpoint: Just use hacks or a generic compiler hint structure. Using alternate implementations would be harder, perhaps a compile time initializer structure. If types were allowed to be looked up from usage/call graph analysis the clutter could perhaps be reduced.

Could some basic boolean logic be enough for a good enough editor experience? And types be implemented in a std library?

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