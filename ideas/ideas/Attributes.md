+++
title= 'Attributes'
summary='Similar to c#'
+++

Copied [from c#](https://learn.microsoft.com/en-us/dotnet/csharp/advanced-topics/reflection-and-attributes/).

Before variables, members, structs, functions etc... a attribute list can be applied. Theese should be seen as named "json like" data that can be used during reflection/compilation.

```csharp
[serializable]
struct Foo
{
};

fun fun_a([in][out] f32 x);
fun fun_b([out][in] f32 x);
fun fun_c([in, out] f32 x);
```

Design thoughts:

- What does it mean to specify a "json like" when no arguments are defined? Would it be up to the type/arguments
- How are the types specified and accessed?
