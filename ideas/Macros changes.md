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

Example foreach loop

```c
#define @foreach(type: Type, name: Ident, container: DynArray<Type>, body: Body)
{
    const size = container.size();
    for(int i=0; i<size; i+=1)
    {
        #emit(body,
            variables: {name: container[i]},
            commands: {
                break: { #emit(break); },
                continue: { #emit(continue); }
                // introduce other like swap_back_delete and push_back? (but could be allowed since adding is well defined)
            }
        );
    }
}
```

Design issues:

- how would scoping work?
- how would emitting work? lots of ambiguity, how to differentate between compile-time and generation
- can all macros we want to implement be implemented with this in a typesafe way? with nice errors/warnings?