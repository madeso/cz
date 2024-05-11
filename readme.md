# cz

CZ is a new programing language inspired by C. This repo contains the specification and reference implementation. The names comes from C and Z is a homeage to Dragonball Z (2 looks like Z and is the last letter and last "release").

What follows is a list of ideas, both ideas where c/c++ could be improved. None of which has been tested.

Roughly the plan is as follows (not necessarily in order):

1. Learn more langauges. In not particular order: more how types and include work in typescript.
2. Learn how zig, odin, rust and ada work in practice (aka implement at least 1 small app/game in each).
3. Implement a reference transpiler and reimplement that app and see areas where it sufferes and can be improved.
4. Evaluate if we(I) should continue on cz or switch efforts to improve the reference langauges the pain points since working on a language with someone is better than working alone.
5. Profit?

## "Pattern matching" on union structs.

This is similar to rust.

## Strong typedefs

## Macros changes

- Macros have return types and arguments, and just like functions they have typpes.
- Types could be regular `string` and `int32` (compile time). But also `Body`, `Statement` and `Definition`. The final specification essentially will depend on how the parser operates.
- They operate on the AST either before or after types have been resolved.
- must start with `@`, for example `@foo` and `@bar`. `ex@mple` is invalid.
- compile time functions generate values, macros generate "code".

The design inspiration here is how react function components generate html from it's arguments.

Example: a simple repeat macro:

```c
#define @repeat(times: int, #body body: Body): Body
{
    for(int i=0; i<times; i+=1) {
        #emit(body);
    }
}
@repeat(4) {print(42);}

// generates
{print(42);}
{print(42);}
{print(42);}
{print(42);}
```

Example: a ifn't macro

```c
#define @ifnt(condition: ()=>bool, #body body: {then: Body, else: Body}): Body
{
    #emit(if(condition() == false));
    #emit(body.then);
    #emit(else body.else);
}
@ifnt(a == b)
{
    then: {print("not same"); },
    else: {print("same"); }
}

// generates
if((a==b) == false)
{print("not same"); }
else {print("same"); }
```

Design issues:

- how would scoping work?
- how would emitting work? lots of ambiguity, how to differentate between compile-time and generation
- can all macros we want to implement be implemented with this in a typesafe way? with nice errors/warnings?

## Keywords may start with `#`

This means we can add new keywords without introducing conflicts

## no include files

- It should work kinda like typescript modules
- Parse C headers to modules
- Modules may accept arguments? (single style headers with define arguments?)

Task: Learn more about typescprip imports.

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

## built in strings, dyn-arrays, optionals, dicts, iterators & tuples

Why? Compiler and IDE can provide better hints.
A possible optimization is that 7/31/63 bit integegers that can be null can be stored within their parent type, without needing additional storage needed. Cleaner syntax when there is only a vector and dictonary.

Counterpoint: Just use hacks or a generic compiler hint structure. Using alternate implementations would be harder, perhaps a compile time initializer structure. If types were allowed to be looked up from usage/call graph analysis the clutter could perhaps be reduced.

Could some basic boolean logic be enough for a good enough editor experience? And types be implemented in a std library?

```c
// sample optional implementation with kotlin like editor hints
struct Optional<T>
{
    union struct {
        None: {}, Value {value: T}
    } data;
    // union of typesafe anonomous structs

    #imply_var {has: bool => .data == .Value;}
    // there is a variable, when it is true .data has to have a value

    fun has_value(): bool
    #imply_result(return == true => has==true)
    // if the return value is true, the has property has to be true
    {
        return data == .Value;
    }

    fun get(): T
    #imply_require(has == true)
    // this function can only be called if has is true
    {
        // if has is true, the declartion of has implies that data is Value and we can access value safely
        return data.value;
    }
};
```

## `?` and `??` operator

Work like c#/kotlin nullable

## Goal: Table driven code generation

Based on [this article](https://www.rfleury.com/p/table-driven-code-generation) and [XState](https://xstate.js.org/) generate code.

With compile-time "macros"/functions, compile-time introspection, "json like" arguments/implicit struct names, and code generation we should be able take a "macro call" and generate code. In the xstate example we could for example generate a function that takes a event and update a "state" object.

## functions on objects

This would support `dynarray.push(...)`.

## buddy (or body) functions / local functions

- Functions inside a function
- Not exposed outside the container function
- Defined after the container function

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

Why? To reduce indenting with 1 step for local functions...

Design issue: can a buddy function call another buddy function? How much do we gain with this compared to just not exposing a function outside the current "module".

## sections inside a function

Works like a function but not named and immidiatly "called"

```c
fun foo(x, y)
{
    var a := x+y;
    use (x, y) {
        // only use x and y, outer variables aren't touched (or read)
        // should modification be legel here? might be more readable to treat everything as const
        x += 3;
        y += x;
        const c = x + 1;
    }
    with (
        const b = x+y;
        const c = ...; // if name match
    );

    return b + a;
}
```

Why? compared to a location function, the local variables comes first and the return values exposed from the function comes after the block. Both code and data follows the logical top to bottom flow.
Design note: should we allow early returns?

## built in test framework

- test local functions?
- test functions that ignore scoping rules

## Unname/ignore identifier

Use the `_` character to

- ignore a return value: `_ = foo();`
- ignore a argument name `fun foo(int _, int _){...}`

## Unnamed functions to be autocompleted

- call a unknown function `.(a, b);` and `.foo(a, b);`

Autocomplete browser/compiler can suggest functions that match the arguments:

- arguments doesn't have to be in the correct order when searching
- additional arguments can be provided

Adding a additional identifier after `.` like `.petCat` can both help the developer with the context what the function is supposed to do. if multiplpe unnamed functions are used. If multiple unnamed functions are used, that graph could be used to find matching function names that would satisify all usages.

I think the goal of the feature is obvious but it would allow a programmer implement a function in a logical way and autocomplete the functions.

If no function can be found, the function can be more safely generated and more easily implemented since it could be called at a later stage it is more likely that both the use case and the types are well known compared to the object oriented `foo.<autocomplete>` workflow.

## Difference between functions and procedures

This terminology isn't reflected in the current state of the document, and outside of this section it's safe to assume whenever just functions are mentioned, that also applies to procedures.

- Functions may not modify arguments
- Functions may work on state but only state local to the function
- Functions may call procedures but only on local variables

Why? This would allow programs to easily transition to more "safe" code since the only side effect a function can have is visible via it's return argument.

Design issue: Can a function print to the console? That is technically a side effect that isn't visible in the code.

## Functions may return anonymous structs

```c
fun foo(): struct {int x;}
{
    return {x: 42};
}
```

Why? Some functions have a specific set of return variables and perhaps it's prefered to not have tuple, but also not need to name this structure due to the return value of `foo` being `FooReturn` would just be clutter.

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

Why? Reads better. This is simlar to how `|` works in the shell but extended to allow the argument to not be the "first" argument.

Design note: use another reference than `$` here. Something like `value` that C# uses for property setters or `ans` that some calculators use. Perhaps a single `#` keyword?

## Sequence-oriented programming

Functional like operators. Would pipeline be sufficient for this.

Task: Investigate with `itertools` from python functions, `<algorithm>` header from c++ and `IEnumerable<T>` methods + extensions from c#.

Task: learn functional programming

## Support both open and closed enum structures

Closed enum structures would be encompass both classical enums and rust enums/unions. "Pattern matching"/matching on type here would be great.

```c
struct Int { int i; };
struct Float { float f; };
struct AnotherFloat { float f; };

enum union Var
{
    Int, Float, AnotherFloat
};

Var v = ...;
switch(v) {
    case Int:
        print(v.i);
        break;
    case Float:
        print(v.f);
        break;
    // compile error: AnotherFloat not matched...
}

```

A open enum would be more a classical interface and virutal functions with inheritence. This is to support adding additional "types" to something that is published.

## `const` vs `mut` vs `let`

- `mut` mutable variable
- `let` runtime constant
- `const` compile time constant

Bit constness work like c++

Design though:

- Compile time functions vs const-correct functions? How are they defined?
- Would it make sense to mark a function "compile time" instead of just running it compile-time?

## Attributes

Copied [from c#](https://learn.microsoft.com/en-us/dotnet/csharp/advanced-topics/reflection-and-attributes/).

Before variables, members, structs, functions etc... a attribute list can be applied. Theese should be seen as named "json like" data that can be used during reflection/compilation.

```csharp
[serializable]
struct Foo
{
};

fun fun_a([in][out] f32 x);
fun fun_b([out][in] f32 x);
fun fun_c([in, out] f32 x);
```

Design thoughts:

- What does it mean to specify a "json like" when no arguments are defined? Would it be up to the type/arguments
- How are the types specified and accessed?

## required argument names

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

## `#embed` keyword

Add data files to app.

```c
const data = #embed "some-file.txt"
```

Design descisions... is it binary or could it be strings too? If so how do we handle character encoding and line endings?

## `#extend` keyword

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

Design issue: How do we handle name collisions? And c function compability?

## Helpful memory management

Introduce concept of owning pointers and explicit move statement. Get inspired by other languages like [vale](https://verdagon.dev/blog/single-ownership-without-borrow-checking-rc-gc)

TBD

## Regex as a native data type

Why? Easily specify compile-time regexes without noise.

Counterpoint: Provide a better library/language integration?

References:

- [Regex engine internals as a library](https://blog.burntsushi.net/regex-internals/)
- [Regex, Part 1: Parser](https://kean.blog/post/regex-parser)
- [Regex, Part 2: Compiler](https://kean.blog/post/regex-compiler)
- [Regex, Part 3: Matcher](https://kean.blog/post/regex-matcher)

## testing

Automatic test discovery (`file.cc` is tested in `file.test.cc`) and catch2 like tests are really nice. Can we support that without overloads and current features?

## Dependency management

External dependencies are forced to specify entry points for all their dependencies.

```kdl
dependencies {
    lib_a "1.5" {
        use {
            lib_b
        }
    }
    lib_b "1.0" directly=false
}
```

Here `lib_b` has to be used even though we don't depend on it. We mark it as `directly=false` as we don't use it directly.

Why?

- Conflicts are visible up-front.
- Libraries with many dependencies are possible but more cumbersome to use. Preasure on libary devs to provide easier to use libraries.

Design decisions:

- Should include/import be used to manage large files?
- Should interface libaries be extempt from this mapping. If so, who decides what a inteface library is and how are conflicting intefaces solved?

# Sample programs

- a small plattform game
- cli tool
- a simple 2d/3d renderer
- ui commands/ctrl+p sample
- json/kdl parser
- jai interpreter
