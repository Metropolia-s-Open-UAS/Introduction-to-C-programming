# Mutable vs Immutable in C#

## 1. Core Definitions

| Aspect | Mutable | Immutable |
|---|---|---|
| Definition | State can be changed after creation | State cannot be changed after creation — any "change" creates a new object |
| Typical implementation | Public setters, methods that modify fields | Read-only fields, no setters, constructor-only initialization |
| Thread safety | Not inherently safe — needs locking for shared access | Inherently thread-safe — no shared mutable state to corrupt |
| Memory behavior | Same object modified in place | Each "modification" allocates a new object |

## 2. Built-in Examples

| Category | Mutable | Immutable |
|---|---|---|
| Text | `StringBuilder` | `string` |
| Collections | `List<T>`, `Dictionary<K,V>`, arrays | `ImmutableList<T>`, `ImmutableArray<T>` (from `System.Collections.Immutable`) |
| Numeric | — | `int`, `double`, `decimal` (all value types are copy-on-assign, effectively immutable per-instance) |
| Date/Time | — | `DateTime`, `TimeSpan` |
| Custom types | Regular `class` with settable properties | `record` (C# 9+), `readonly struct`, class with only `get`-only properties |

## 3. `string` — The Classic Immutable Example

| Operation | What actually happens |
|---|---|
| `string s = "Hello";` | Creates a string object `"Hello"` on the heap |
| `s = s + " World";` | Does **not** modify the original — creates a **new** string `"Hello World"`, reassigns `s` to point to it |
| `s.ToUpper();` | Returns a new string; the original `s` is unchanged unless reassigned |
| Repeated concatenation in a loop | Each `+=` allocates a new string — inefficient for many operations |

```csharp
string s1 = "Hello";
string s2 = s1;
s1 += " World";
Console.WriteLine(s1); // "Hello World"
Console.WriteLine(s2); // "Hello" — s2 still points to the original, untouched object
```

**For heavy string building, use the mutable `StringBuilder` instead:**

```csharp
StringBuilder sb = new StringBuilder("Hello");
sb.Append(" World"); // modifies the same object in place — no new allocation each time
Console.WriteLine(sb.ToString());
```

## 4. Creating Immutable Custom Types

| Technique | Syntax | Notes |
|---|---|---|
| Read-only fields | `private readonly int age;` | Assignable only in constructor or declaration |
| Get-only properties | `public int Age { get; }` | No `set`; must be assigned in constructor |
| `init` accessor (C# 9+) | `public int Age { get; init; }` | Settable only during object initialization, not after |
| `record` type (C# 9+) | `public record Person(string Name, int Age);` | Immutable by default, includes value-based equality, `with` expressions |
| `readonly struct` | `public readonly struct Point { public readonly int X; }` | Guarantees the struct itself can't be mutated after creation |

```csharp
class PersonImmutable
{
    public string Name { get; }
    public int Age { get; }

    public PersonImmutable(string name, int age)
    {
        Name = name;
        Age = age;
    }
}
// PersonImmutable p = new PersonImmutable("Sara", 25);
// p.Age = 26; // Compile error — no setter available
```

```csharp
public record Person(string Name, int Age);

Person p1 = new Person("Sara", 25);
Person p2 = p1 with { Age = 26 }; // creates a NEW record with Age changed; p1 unchanged
```

## 5. Mutable Custom Types (For Comparison)

```csharp
class PersonMutable
{
    public string Name { get; set; }
    public int Age { get; set; }
}

PersonMutable p = new PersonMutable { Name = "Sara", Age = 25 };
p.Age = 26; // modifies the same object directly
```

## 6. Why Immutability Matters

| Benefit | Explanation |
|---|---|
| Thread safety | No locks needed — immutable objects can be freely shared across threads without race conditions |
| Predictability | An object's state never changes unexpectedly from somewhere else in the code (no aliasing bugs) |
| Safe as dictionary keys | Mutable objects used as keys can break hash-based lookups if their hash-relevant fields change after insertion |
| Easier debugging | You can trust that a reference passed around still holds its original values |
| Functional-style code | Encourages returning new values instead of side effects — pairs well with LINQ |

| Trade-off | Explanation |
|---|---|
| Extra allocations | Every "change" creates a new object — can add GC pressure for frequent updates |
| More verbose construction | Often requires constructor parameters for every field instead of simple property assignment |

## 7. Quick Decision Guide

| Situation | Use |
|---|---|
| Value shared across threads or passed widely | Immutable (`record`, read-only properties) |
| Frequently updated in place (e.g., a running total, UI state) | Mutable (`class` with setters) |
| Building a string through many concatenations | `StringBuilder` (mutable) |
| Representing a simple data value that shouldn't change (DTO, config, coordinates) | Immutable (`record`, `readonly struct`) |
| Object used as a dictionary/hash-set key | Immutable — mutating it after insertion breaks lookups |
| Domain entities with changing state (e.g., `Order` whose `Status` changes over time) | Mutable `class` |

## 8. Summary Table

| | Mutable | Immutable |
|---|---|---|
| Can change after creation | Yes | No |
| Thread-safe by default | No | Yes |
| Common C# types | `List<T>`, `StringBuilder`, custom classes with setters | `string`, `record`, `readonly struct` |
| "Modify" operation cost | Cheap (in-place update) | Allocates new object |

