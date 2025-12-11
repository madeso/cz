---
title: "Operator overloading"
summary: "How to define and introduce new operators"
tags:
    - questionable
    - operators
---

Note: I'm not sure if this is a good idea or not.

WHat if all operators are implemented as a special syntax that uses a macro type.

```
const u8 a = @.math(b + c);
```

Here `@.` would start the special parsing and use the `math` operators. One could define custom operators and extend the math library.

```
const vec3 a = @.vec.math(b dot c);
```