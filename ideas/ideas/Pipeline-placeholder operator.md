---
title: "Pipeline-placeholder operator"
summary: "Use `|> $` to chain function calls"
tags:
  - from-twitter
  - for-functions
---

https://twitter.com/seanbax/status/1654121073053511682

```c
const x = foo()
    |> bar($)
    ;
```

versus

```c
const x = bar(foo());
```

### Why?

- It reads better.
- This is also simlar to how `|` works in the shell but extended to allow the argument to not be the "first" argument.

### Design note

* Use another reference than `$` here. Something like `value` that C# uses for property setters or `ans` that some calculators use. Perhaps a single `#` keyword?
* If `$` is not provided and line is a single "value", then treat it as sugar for passing the value as a argument: `const x = foo() |> bar`

### See also
* {{<link "Nullish coalescing operators.md">}}
* {{<link "Pattern matching on union structs.md">}}

