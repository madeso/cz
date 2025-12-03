---
title: 'Table driven code generation'
summary: 'Should other code generations also be supported'
tags:
    - code-generation
    - editor
    - xstate
---

Based on [this article](https://www.rfleury.com/p/table-driven-code-generation) and [XState](https://xstate.js.org/) generate code.

With compile-time "macros"/functions, compile-time introspection, "json like" arguments/implicit struct names, and code generation we should be able take a "macro call" and generate code. In the xstate example we could for example generate a function that takes a event and update a "state" object.