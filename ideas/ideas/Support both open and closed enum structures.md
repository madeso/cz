---
title: 'Open and closed enum structures'
summary: 'Rust enums vs a oop interface'
---

## Closed enum
Closed enum structures would be encompass both classical enums and rust enums/unions. "Pattern matching"/matching on type here would be great.

```c
struct Int { int i; };
struct Float { float f; };
struct AnotherFloat { float f; };

enum union Var
{
    Int, Float, AnotherFloat
};

Var v = ...;
switch(v) {
    case Int:
        print(v.i);
        break;
    case Float:
        print(v.f);
        break;
    // compile error: AnotherFloat not matched...
}

```

## Open enum
A open enum would be more a classical interface and virutal functions with inheritence. This is to support adding additional "types" to something that is published.