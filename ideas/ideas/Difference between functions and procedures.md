---
title: "Functions vs Procedures"
summary: "Gradually transform a codebase into a more functional"
tags:
  - declaration
  - for-functions
---

### Difference between functions and procedures

This terminology isn't reflected in the current state of the document, and outside of this section it's safe to assume whenever just functions are mentioned, that also applies to procedures.

- Functions may not modify arguments
- Functions may work on state but only state local to the function
- Functions may call procedures but only on local variables

### Why?

This would allow programs to easily transition to more "safe" code since the only side effect a function can have is visible via it's return argument.

### Design issue

Can a function print to the console? That is technically a side effect that isn't visible in the code.
