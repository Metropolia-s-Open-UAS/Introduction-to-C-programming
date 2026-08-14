# Value Types vs Reference Types in C#

## 1. Core Definitions

| Aspect | Value Type | Reference Type |
|---|---|---|
| What it stores | The actual data itself | A reference (pointer) to data stored elsewhere (heap) |
| Keyword to declare | `struct`, `enum` | `class`, `interface`, `delegate`, `record` (by default) |
| Memory location | Stack (or inline within containing object) | Heap (the object); the reference itself may live on stack |
| Default value | Zero/empty equivalent (`0`, `false`, `'\0'`) — never `null` unless `Nullable<T>` | `null` |
| Can be `null`? | No (unless declared `Nullable<T>` / `int?`) | Yes |

## 2. Built-in Examples

| Category | Value Types | Reference Types |
|---|---|---|
| Numeric | `int`, `double`, `float`, `decimal`, `long`, `byte`, `short` | — |
| Other primitives | `bool`, `char` | `string` (behaves value-like but is actually a reference type) |
| Custom types | `struct`, `enum` | `class`, `interface`, `delegate` |
| Collections | — | `array`, `List<T>`, `Dictionary<K,V>` |
| Special | `Nullable<T>` (`int?`) | `object` |

## 3. Assignment Behavior

| Type | `a = b` Behavior | Example |
|---|---|---|
| Value type | Copies the actual value — two independent copies | `int a = 5; int b = a; b = 10;` → `a` is still `5` |
| Reference type | Copies the reference — both variables point to the same object | `Car a = new Car(); Car b = a; b.Model = "X";` → `a.Model` is also `"X"` |

```csharp
struct PointS { public int X; }
class PointC { public int X; }

PointS ps1 = new PointS { X = 1 };
PointS ps2 = ps1;
ps2.X = 99;
Console.WriteLine(ps1.X); // 1 — unaffected

PointC pc1 = new PointC { X = 1 };
PointC pc2 = pc1;
pc2.X = 99;
Console.WriteLine(pc1.X); // 99 — same object
```

## 4. Passing to Methods

| Type | Default behavior | With `ref`/`out` |
|---|---|---|
| Value type | Passed by value — method gets a copy; changes don't affect the original | `ref`/`out` makes it act like a reference — changes DO affect original |
| Reference type | The reference is passed by value — method can modify the object's fields, but reassigning the parameter itself doesn't affect the caller's variable | `ref` on a reference type lets you reassign what the caller's variable points to |

```csharp
void ModifyValue(int x) { x = 100; }
void ModifyRef(Car c) { c.Model = "Changed"; }        // mutates the shared object
void ReassignRef(Car c) { c = new Car(); }            // does NOT affect caller's variable
void ReassignRefWithRef(ref Car c) { c = new Car(); } // DOES affect caller's variable
```

## 5. Equality Comparison

| Type | `==` Default Behavior | Notes |
|---|---|---|
| Value type | Compares actual values field-by-field (for `struct`, unless overridden) | `int`, `bool`, etc. always compare by value |
| Reference type | Compares references (are they the same object in memory?) | Override `Equals()`/`==` to compare by value instead (e.g., `string` already does this) |

```csharp
Car c1 = new Car { Model = "Tesla" };
Car c2 = new Car { Model = "Tesla" };
Console.WriteLine(c1 == c2); // False — different objects, even with same data

string s1 = "hello";
string s2 = "hello";
Console.WriteLine(s1 == s2); // True — string overrides == to compare content
```

## 6. Nullability

| Type | Can be null? | Workaround |
|---|---|---|
| Value type | No | `int? x = null;` uses `Nullable<T>` wrapper |
| Reference type | Yes, by default | Nullable reference types (`string?`) added in C# 8 for compile-time null-warnings only |

## 7. Boxing and Unboxing

| Term | Definition | Example |
|---|---|---|
| Boxing | Converting a value type into an `object` (heap-allocated wrapper) | `int i = 5; object o = i;` |
| Unboxing | Extracting the value type back out of the `object` | `int j = (int)o;` |
| Performance cost | Boxing/unboxing has overhead — allocates on heap, copies data | Avoid in hot loops (e.g., non-generic `ArrayList` boxes every element) |

## 8. When to Use `struct` vs `class`

| Use `struct` when... | Use `class` when... |
|---|---|
| The type is small (rule of thumb: ≤16 bytes) | The type is large or complex |
| It represents a single value (e.g., `Point`, `Color`, `Vector2`) | It represents an entity with identity (e.g., `Customer`, `Order`) |
| It's immutable or rarely mutated | It needs to be mutated and shared across references |
| Short-lived, created/discarded frequently | Long-lived, or needs inheritance |
| You want to avoid GC pressure | You need polymorphism (`virtual`/`override`, inheritance) |
| No inheritance needed (structs can't inherit from another struct/class) | Inheritance hierarchy is needed |

## 9. Quick Summary

| | Value Type | Reference Type |
|---|---|---|
| Stored | Stack (typically) | Heap |
| Copied on assignment | Full data | Just the reference |
| Default | Zero-equivalent | `null` |
| Examples | `int`, `struct`, `enum`, `bool` | `class`, `string`, `array`, `List<T>` |

