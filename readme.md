# cz

CZ is a new programing language inspired by C. This repo contains the specification and reference implementation. The names comes from C and Z is a homeage to Dragonball Z (2 looks like Z and is the last letter and last "release").


## "Pattern matching" on union structs.
This is similar to rust.

## Strong typedefs

## Macros changes
* Macros have "return" types (string, body, statement, definition)
* must start with `@`, for example `@foo` and `@bar`. `ex@mple` is invalid.

## Keywords may start with `#`
This means we can add new keywords without introducing conflicts

## no include files
* It should work kinda like typescript modules
* Parse C headers to modules
* Modules may accept arguments? (single style headers with define arguments?)

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
*todo*: is `sg.` required or is `sg` enough?

## built in strings, dyn-arrays, dicts, iterators & tuples

## functions on objects

## buddy (or body) functions / local functions
* Functions inside a function
* Not exposed outside the container function
* Defined after the container function
```c
fun foo()
{
    bar();
}
#fun bar()
{
    // ...
}
```

## sections inside a function
* like a function but not named and immidiatly called

```c
fun foo(x, y)
{
    var a := x+y;
    use x, y {
        // only use x and y, outer variables aren't touched (or read)
        x += 3;
        y += x;
        // can use multiple use returns, var names must match
        use return x+y as b;
    }

    return b + a;
}
```

## built in test framework
* test local functions?
* test functions that ignore scoping rules

## Unname/ignore identifier
Use the `_` character to
* ignore a return value: `_ = foo();`
* ignore a argument name `fun foo(int _, int _){...}`
* call a unknown function `_(a, b);`, autocomplete/compiler can suggest functions that match the arguments.

## Difference between functions and procedures
* Functions may not modify arguments
* Functions may work on state but only state local to the function
* Functions may call procedures but only on local variables

## Functions may return anonymous structs
```c
fun foo(): struct {int x;}
{
    return {x: 42};
}```

## Pipeline-placeholder operator
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

## `?` and `??` operator
Work like c#/kotlin nullable

## `const` vs `var`
Bit constness work like c++


## `#embed` keyword
Add data files to app.
```c
const data = #embed "some-file.txt"
```

## `@extend` keyword
Works like struct embedding in Golang

```c
struct Foo
{
    int x;
}

struct Bar @extend Foo
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

## Overloading and function/oop syntax?

The following code examples are the same

```c
struct Foo
{
    proc bar()
    {
    }
}

// ...

Foo foo = ...;
bar(foo);
```

```cpp
struct Foo
{
}

proc bar(this: Foo)
{
}

// ...

Foo foo = ...;
foo.bar();
```

ie "member" functions are only syntax sugar for functions taking the first struct as a argument, and `foo.bar()` is only syntax sugar for calling `bar` with the first argument outside of the argument list.
Member access has higher priority, use `->` syntax to only access functions: `foo->name.space()` is sugar for `name.space(foo)` not `space(foo.name)`


## Helpful memory management
Instroduce concept of owning pointers and explicit move statement. Get inspired by other languages like [vale](https://verdagon.dev/blog/single-ownership-without-borrow-checking-rc-gc)

TBD

