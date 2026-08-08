#### Conditional Statements in C# / .NET

#### 1. Basic Conditional Constructs

| Construct | Syntax | Description | Example |
|---|---|---|---|
| `if` | `if (condition) { }` | Executes block if condition is `true` | `if (x > 0) { Console.WriteLine("Positive"); }` |
| `if...else` | `if (cond) {} else {}` | Two-way branch | `if (x > 0) {...} else {...}` |
| `if...else if...else` | Chained `if` | Multi-way branch, evaluated top to bottom | `if (x>0){...} else if (x==0){...} else {...}` |
| `switch` statement | `switch (expr) { case v: ... break; }` | Multi-way branch on a value/pattern | See below |
| `switch` expression (C# 8+) | `var y = expr switch { pattern => value, ... };` | Expression-based switch, returns a value | See below |
| Ternary `?:` | `cond ? valA : valB` | Compact if/else returning a value | `string r = x > 0 ? "Pos" : "Neg";` |
| Null-coalescing `??` | `a ?? b` | Returns `a` if not null, else `b` | `string name = input ?? "default";` |
| Null-coalescing assignment `??=` | `a ??= b` | Assigns `b` to `a` only if `a` is null | `list ??= new List<int>();` |
| Null-conditional `?.` / `?[]` | `obj?.Member` | Skips member access if `obj` is null (returns null) | `int? len = str?.Length;` |

#### 2. `switch` Statement — Classic Syntax

| Element | Example | Notes |
|---|---|---|
| Case label | `case 1:` | Must be constant (or pattern in C# 7+) |
| Fallthrough | `case 1: case 2: DoWork(); break;` | Empty cases can stack; non-empty cases need explicit jump |
| Default | `default: break;` | Optional, runs if no case matches |
| Exit | `break;`, `return;`, `goto case X;` | Required at end of each non-empty case block |
| Pattern matching (C# 7+) | `case int n when n > 0:` | `when` clause adds a guard condition |
| Type pattern | `case string s:` | Matches by runtime type, binds variable `s` |

```csharp
switch (shape)
{
    case Circle c when c.Radius > 10:
        Console.WriteLine("Big circle");
        break;
    case Circle c:
        Console.WriteLine("Circle");
        break;
    case Square s:
        Console.WriteLine("Square");
        break;
    default:
        Console.WriteLine("Unknown");
        break;
}
```

#### 3. `switch` Expression (C# 8+)

| Feature | Syntax | Purpose |
|---|---|---|
| Basic arm | `x switch { 1 => "one", 2 => "two", _ => "other" }` | Returns a value directly |
| Discard `_` | `_ => defaultValue` | Acts as default case |
| Property pattern | `p switch { { Age: > 18 } => "adult", _ => "minor" }` | Matches on object properties |
| Tuple pattern | `(a, b) switch { (0, 0) => "origin", _ => "other" }` | Matches on tuple combinations |
| Relational pattern (C# 9+) | `n switch { < 0 => "neg", 0 => "zero", > 0 => "pos" }` | Comparison-based matching |
| Logical patterns (C# 9+) | `n switch { > 0 and < 10 => "small", _ => "other" }` | `and`, `or`, `not` combinators |

```csharp
string category = age switch
{
    < 13 => "Child",
    >= 13 and < 20 => "Teen",
    >= 20 => "Adult",
    _ => "Unknown"
};
```

#### 4. Pattern Matching Keywords (used inside `if`, `switch`, `is`)

| Pattern | Example | Matches when... |
|---|---|---|
| Type pattern | `obj is string s` | `obj` is of type `string`; binds to `s` |
| Constant pattern | `x is 5` | Value equals constant |
| Relational pattern | `x is > 0` | Comparison holds |
| Logical `and`/`or`/`not` | `x is > 0 and < 100` | Combined conditions |
| Property pattern | `p is { Name: "Sam" }` | Object's property matches |
| Positional (deconstruction) | `point is (0, 0)` | Deconstructed values match |
| `var` pattern | `obj is var x` | Always matches; binds variable |

#### 5. Quick Comparison — When to Use What

| Scenario | Recommended Construct |
|---|---|
| Simple true/false branch | `if / else` |
| Returning a value based on a condition | Ternary `?:` or `switch` expression |
| Many discrete values of same variable | `switch` statement/expression |
| Type-based branching | `switch` with type patterns, or `is` |
| Null handling / defaults | `??`, `??=`, `?.` |
| Complex conditions with ranges/combinators | `switch` expression with relational/logical patterns |
| One-off inline null check | `?.` or `is null` |

