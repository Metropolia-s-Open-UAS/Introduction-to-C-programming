#### Primitive vs Non-Primitive Types in C#

#### 1. Core Definitions

| Aspect | Primitive Types | Non-Primitive Types |
|---|---|---|
| Definition | Basic, built-in data types provided directly by the language/CLR | Types built from primitive types or other objects — user-defined or complex built-in types |
| Also called | "Simple types" / "Built-in value types" | "Reference types" / "Derived types" / "Complex types" |
| Size | Fixed, predetermined by the CLR | Variable — depends on contents |
| Defined by | The language itself (C#/.NET) | The programmer, or the .NET Framework Class Library |
| Memory | Typically stack (value types) | Typically heap (reference types) |

> **Note:** "Primitive type" isn't an official C# language term (C# spec calls them "simple types"), but it's commonly used this way in teaching/interviews, contrasted with "non-primitive" (arrays, classes, strings, etc.).

#### 2. Primitive Types in C#

| Category | Types |
|---|---|
| Integer | `byte`, `sbyte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong` |
| Floating-point | `float`, `double` |
| Decimal | `decimal` |
| Boolean | `bool` |
| Character | `char` |

```csharp
int age = 25;
double price = 19.99;
bool isActive = true;
char grade = 'A';
```

#### 3. Non-Primitive Types in C#

| Category | Types/Examples |
|---|---|
| Text | `string` |
| Collections | `array`, `List<T>`, `Dictionary<K,V>`, `Queue<T>`, `Stack<T>` |
| User-defined | `class`, `struct`, `enum`, `interface`, `record`, `delegate` |
| Special | `object` |

```csharp
string name = "Amir";
int[] scores = { 90, 85, 77 };
List<string> names = new List<string> { "Amir", "Sara" };

class Car { public string Model; }
Car myCar = new Car();
```

#### 4. Key Behavioral Differences

| Aspect | Primitive | Non-Primitive |
|---|---|---|
| Storage location | Stack (as value types) | Heap (reference types) — except `struct`, which is non-primitive but still a value type |
| Can be `null`? | No (unless `Nullable<T>`) | Yes (except `struct`) |
| Created by | Language keywords directly (`int x = 5;`) | Usually via `new` keyword (`new Car()`), or literals for `string`/`array` |
| Default value | Zero-equivalent (`0`, `false`, `'\0'`) | `null` (for reference types) |
| Has built-in operators (`+`, `-`, etc.) | Yes, natively supported | Only if explicitly overloaded (operator overloading) |
| Defined by | .NET runtime/CLR itself | The class library or your own code |

#### 5. Important Edge Cases

| Type | Primitive or Non-Primitive? | Why |
|---|---|---|
| `string` | Non-primitive | It's a reference type, even though it feels "basic"; internally it's a `class` (`System.String`) |
| `struct` | Non-primitive | User-definable, even though it behaves like a value type (stack-stored) |
| `enum` | Non-primitive | User-defined named constants, even though it's a value type under the hood |
| `object` | Non-primitive | Base type for everything, but not itself a "basic" building-block type |
| `decimal` | Primitive | Simple type in the C# spec, despite being 128-bit and more complex internally |

#### 6. Quick Summary Table

| | Primitive | Non-Primitive |
|---|---|---|
| Built into the language | Yes | No (built from primitives/objects) |
| Examples | `int`, `bool`, `char`, `double` | `string`, `array`, `class`, `List<T>` |
| Storage | Stack | Heap (mostly) |
| Complexity | Single value | Composed of multiple values/behaviors |

