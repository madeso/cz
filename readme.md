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

## Implicit struct names 
```c
sg_setup(&{
    .logger.func = slog_func,
});
```
vs
```c
sg_setup(&(sg_desc){
    .logger.func = slog_func,
});
```

## no include files
* It should work kinda like typescript modules
* Parse C headers to modules
* Modules may accept arguments? (single style headers with define arguments?)

## built in strings, dyn-arrays, dicts, iterators & tuples

## functions on objects

## buddy (or body) functions / local functions
* Functions inside a function
* Not exposed outside the container function
* Defined after the container function
```
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
* can't nest a sections
* don't indent sections

```
fun foo(x, y)
{
    use x, y
    // only use x and y, outer variables aren't touched
    x += 3;
    y += x;
    // can use multiple use returns, vars must match
    use return a as x+y;
    end

    return x + a;
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
* Functions may not call procedures

```
proc foo() {}
#proc buddy_foo() {}

fun bar() {}
#fun budddy_bar() {}
```

