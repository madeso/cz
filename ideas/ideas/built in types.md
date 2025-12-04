---
title: "built in types"
summary: "strings, dyn-arrays, optionals, dicts, iterators & tuples"
tags:
  - for-types
---

### About

Should the "types" be built in?

Types originally referred to strings, dyn-arrays, optionals, dicts, iterators & tuples, but perhaps also should include primitve types such as `i32` and `f32`. The advantage is that there would be no special rules and all types would work the same.

### Why?

Compiler and IDE can provide better hints. A possible optimization is that 7/31/63 bit integegers that can be null can be stored within their parent type, without needing additional storage needed. Cleaner syntax when there is only a vector and dictonary.

### Counterpoint

Just use hacks or a generic compiler hint structure. Using alternate implementations would be harder, perhaps a compile time initializer structure. If types were allowed to be looked up from usage/call graph analysis the clutter could perhaps be reduced.

### Alternative

Could some basic boolean logic be enough for a good enough editor experience? And types be implemented in a std library? For example using {{<link "./state-hints.md" >}}
