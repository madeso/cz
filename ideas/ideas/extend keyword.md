---
title: 'Struct embedding'
summary: 'using the `#extend` keyword'
tags:
    - hash-keywords
    - for-types
    - keywords
---

Works like struct embedding in Golang

```c
struct Foo
{
    int x;
}

struct Bar #extend Foo
{
   int y;
}

var bar := Foo{...};
bar.x = bar.y;
```

```c
proc foo() {}
#proc buddy_foo() {}

fun bar() {}
#fun budddy_bar() {}
```