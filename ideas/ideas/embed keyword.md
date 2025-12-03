---
title: 'Embed data'
summary: 'using the `#embed` keyword'
---

Add data files to app.

```c
const data = #embed "some-file.txt"
```

Design descisions... is it binary or could it be strings too? If so how do we handle character encoding and line endings?