+++
title='Resolving dependency collisions/diamond pattern'
summary='by specifing dependencies'
+++

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