---
title: bitset
summary: Mark variable and/or type as a bitset to only allow bit shifting on that variable.
---

Mark variable and/or type as a bitset to only allow bit shifting on that variable.

```cpp
enum Bits {
    A = 1 << 0,
    B = 1 << 1,
    C = 1 << 2
}
bitset u32 a = Bits.A;
bitset u32 b = Bits.B;
bitset u32 c = a | b;
```

```cpp
bitset enum Bits {
    A,
    B,
    C
    // auto counted the bits
}
Bits a = Bits.A;
Bits b = Bits.B;
Bits c = a | b;
```