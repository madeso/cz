---
title: 'Pipeline-placeholder operator'
summary: 'Use `|> $` to chain function calls'
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

Why? Reads better. This is simlar to how `|` works in the shell but extended to allow the argument to not be the "first" argument.

Design note: use another reference than `$` here. Something like `value` that C# uses for property setters or `ans` that some calculators use. Perhaps a single `#` keyword?