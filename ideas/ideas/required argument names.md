---
title: 'Required/named argument names'
summary: 'Copied from switft'
---

This is copied from swift, not yet sure of the exact syntax. I've tried to describe swift below:

```c
fun write_log(message: string, prefix: string);
write_log("error message", prefix: ">>>");
```

Here all arguments must be named, except the first.

```c
func write_log(message message: string, withPrefix prefix: string);
write_log(message: "QWERTY", withPrefix: "***", andSuffix: "$$$")
```

The arguments are now `message` and `prefix`. Since message is specified is is now required. The order is `published_name` followed by the `internal_name`.

In swift the first name rule doesn't apply to constructors.

You can avoid having a named argument by setting the `published_name` to `_`:

```
fun write_log(message: string, _ prefix: string);
write_log("error message", ">>>");
```

Design thoughts:

- Should parameter names be allowed even though they aren't required?
- Should named arguments be part of the the overload
- The inconsequent first/rest arguments is weird
- Should the published name be specified in a attribute?
- In what order are arguments evaluated? Should argument order be specified in general? What does zig and odin do? Should order always be left->right and we can supply a `#allow_reorder` prefix when calling a function to allow for optimization...