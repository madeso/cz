## Overloading and function/oop syntax?

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

Design issue: How do we handle name collisions? And c function compability?