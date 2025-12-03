---
title: Getter markup
summary: Enforces that getters are simple
---
This enforces that a "get" function that does complicated work can't be named get. 

```csharp
[get]
int get_name()
{
    return this.name;
}
```

Does this need new grammar or just a regular attribute with some linting rules?
