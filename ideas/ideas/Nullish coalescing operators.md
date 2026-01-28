---
title: 'Nullish coalescing operators'
summary: '`?` and `??` operator'
tags:
    - from-csharp
    - from-typescript
    - from-kotlin
    - for-types
---

Work like c#/kotlin nullable

## Design note:
* Can it be extended this works for other than null and a union?

```ts
const x : string | int = foo;
const y : string | float = foo ?? if float: $/2.0;
```

### See also
* {{<link "Pipeline-placeholder operator.md">}}
* {{<link "Pattern matching on union structs.md">}}