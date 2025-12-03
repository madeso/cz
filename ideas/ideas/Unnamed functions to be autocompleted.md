---
title: 'Unnamed functions to be autocompleted'
summary: 'Specify arguments first and then find a matching function'
tags:
    - editor
---

## Unnamed functions to be autocompleted

- call a unknown function `.(a, b);` and `.foo(a, b);`

Autocomplete browser/compiler can suggest functions that match the arguments:

- arguments doesn't have to be in the correct order when searching
- additional arguments can be provided

Adding a additional identifier after `.` like `.petCat` can both help the developer with the context what the function is supposed to do. if multiplpe unnamed functions are used. If multiple unnamed functions are used, that graph could be used to find matching function names that would satisify all usages.

I think the goal of the feature is obvious but it would allow a programmer implement a function in a logical way and autocomplete the functions.

If no function can be found, the function can be more safely generated and more easily implemented since it could be called at a later stage it is more likely that both the use case and the types are well known compared to the object oriented `foo.<autocomplete>` workflow.