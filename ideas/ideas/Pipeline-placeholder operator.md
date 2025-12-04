---
title: 'Pipeline-placeholder operator'
summary: 'Use `|> $` to chain function calls'
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

## Why?
* It reads better.
* This is also simlar to how `|` works in the shell but extended to allow the argument to not be the "first" argument.

## Design note
Use another reference than `$` here. Something like `value` that C# uses for property setters or `ans` that some calculators use. Perhaps a single `#` keyword?