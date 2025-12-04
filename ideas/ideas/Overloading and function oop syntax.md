---
title: 'Overloading and function/oop syntax?'
summary: 'Should this be available'
tags:
    - oop
    - for-types
    - from-csharp
---

The following code examples are the same

```c
struct Foo
{
    proc bar()
    {
    }
}

// ...

Foo foo = ...;
bar(foo);
```

```cpp
struct Foo
{
}

proc bar(this: Foo)
{
}

// ...

Foo foo = ...;
foo.bar();
```

ie "member" functions are only syntax sugar for functions taking the first struct as a argument, and `foo.bar()` is only syntax sugar for calling `bar` with the first argument outside of the argument list.

Member access has higher priority, use `->` syntax to only access functions: `foo->name.space()` is sugar for `name.space(foo)` not `space(foo.name)`

Can we use something like [c# extension methods](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/extension-methods) to differentiate member functions and non member functions.

## See also
* {{<link "Pipeline-placeholder operator.md">}}
* {{<link "../references/non-member-functions.md">}}

### Design issue
How do we handle name collisions? And c function compability?