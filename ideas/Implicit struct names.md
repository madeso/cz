## Implicit struct names

```c
sg.setup(&{
    .logger.func = slog_func,
});
```

vs

```c
sg.setup(&(sg.desc){
    .logger.func = slog_func,
});
```

Optionally use namespaces/imports to differentiate/be explicit

```c
sg.setup(&sg.{
    .logger.func = slog_func,
});
```

_todo_: is `sg.` required or is `sg` enough? How does zig and odin handle this?

Design note: it would be preferable if it was easy to parse so we can provide in-editor hints and special editors like XState