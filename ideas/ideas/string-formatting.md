---
title: "Built in string formatting"
summary: " "
---
Add syntax for constructing formatted strings. It would be nice if it also handled custom markup for console coloring and template strings like.

### swift
```swift
let temperature = 39
let weatherStatement = "The temperature is \(temperature) degrees."
```
https://www.dhiwise.com/post/understanding-swift-strings-manipulating-text-in-swift

### c#

```csharp
var name = "Mark";
var date = DateTime.Now;

Console.WriteLine("Hello, {0}! Today is {1}, it's {2:HH:mm} now.", name, date.DayOfWeek, date);
Console.WriteLine($"Hello, {name}! Today is {date.DayOfWeek}, it's {date:HH:mm} now.");
```
https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/interpolated

Console color markup
```csharp
AnsiConsole.Markup("[maroon on blue]Hello[/]").
AnsiConsole.Markup("[underline red]Hello[/] World!");
```
https://spectreconsole.net/

### c++

```
fmt::print("The answer is {}.", 42);
```
https://fmt.dev/12.0/syntax/

### js/ts
Javascript/typescript uses backtick
```ts
const arg = "argument";
const str = `This is a formatted string ${argument}`
```

### Python
Python uses prefixes
```python
```
which is nice with "template" t-strings to solve "bobby tables" vulnerability

```python
from my_database_library import execute_sql

def get_student(name: str) -> dict:
    query = f"SELECT * FROM students WHERE name = '{name}'"
    return execute_sql(query)

get_student("Robert'); DROP TABLE students;--")
```

vs the safe version

```python
from string.templatelib import Template
from my_database_library import execute_sql_t

def get_student(name: str) -> dict:
    query = t"SELECT * FROM students WHERE name = '{name}'"
    return execute_sql_t(query)

get_student("Robert'); DROP TABLE students;--")
```

where the query variable instead of being a string is a "template" type that users can parse.
```ts
using Template = {type: 'interpolation', value: string} | string;
```

https://davepeck.org/2025/04/11/pythons-new-t-strings/