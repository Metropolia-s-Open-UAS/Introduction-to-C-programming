# Stack vs Heap Memory in C# / .NET

## 1. Core Differences

| Aspect | Stack | Heap |
|---|---|---|
| Structure | LIFO (Last In, First Out) — like a stack of plates | Free-form region, managed dynamically |
| Storage | Value types, method call frames, references (pointers) themselves | Reference type objects, boxed value types |
| Allocation speed | Very fast — just moves a pointer | Slower — requires finding free memory block |
| Deallocation | Automatic — frees when method returns (scope ends) | Handled by Garbage Collector (GC) — not immediate |
| Size | Small, fixed at thread creation (~1MB default) | Large, limited mainly by available system RAM |
| Memory management | Automatic, deterministic | Automatic but non-deterministic (GC decides when) |
| Thread safety | Each thread has its own stack | Heap is shared across all threads in the process |
| Access speed | Faster (CPU cache-friendly, contiguous) | Slightly slower (scattered allocations) |
| Risk | `StackOverflowException` (deep/infinite recursion) | `OutOfMemoryException` (rare, large allocations) |

## 2. What Goes Where in C#

| Type | Stored On | Notes |
|---|---|---|
| `int`, `double`, `bool`, `char`, `struct` (value types) | Stack | Stored directly, copied by value |
| Local variables (method scope) | Stack | Includes value type locals and object *references* |
| `class` instances (reference types) | Heap | The object's data lives on heap; a reference/pointer to it lives on stack |
| `string` | Heap | Reference type, even though it behaves value-like (immutable) |
| Array (`int[]`, `object[]`, etc.) | Heap | Arrays are always reference types, regardless of element type |
| Boxed value types | Heap | `object o = 5;` copies the `int` onto the heap ("boxing") |
| Static fields | Heap (in a special area tied to the type) | Lives for the app's lifetime |
| Captured variables in closures/lambdas | Heap | Compiler moves them into a hidden class instance |

## 3. Example Walkthrough

```csharp
void Method()
{
    int x = 10;              // x: stored on stack
    Car myCar = new Car();   // myCar (reference): on stack
                              // the actual Car object: on heap
}
```

| Line | What happens |
|---|---|
| `int x = 10;` | Value `10` stored directly on the stack |
| `Car myCar = new Car();` | `new Car()` allocates the object on the heap; the variable `myCar` (a reference/pointer to that heap location) is stored on the stack |
| Method returns | `x` and `myCar` (the reference) are popped off the stack immediately — but the `Car` object on the heap stays until the GC determines nothing references it anymore |

## 4. Value Types vs Reference Types — Behavior Difference

| Behavior | Value Type (struct, stack) | Reference Type (class, heap) |
|---|---|---|
| Assignment (`a = b`) | Copies the actual data | Copies the reference (both point to same object) |
| Passing to a method | Passed by value (a copy) — changes inside method don't affect original, unless `ref`/`out` used | Passed by reference — changes to the object's fields ARE visible outside the method |
| Equality (`==`) | Compares values | Compares references (unless overridden) by default |

```csharp
struct PointS { public int X; }
class PointC { public int X; }

PointS s1 = new PointS { X = 5 };
PointS s2 = s1;
s2.X = 100;
// s1.X is still 5 — separate copies on the stack

PointC c1 = new PointC { X = 5 };
PointC c2 = c1;
c2.X = 100;
// c1.X is now 100 too — both variables reference the same heap object
```

## 5. Why This Matters (Practical Impact)

| Concern | Explanation |
|---|---|
| Performance | Excessive heap allocations (e.g., creating many small objects in a loop) increase GC pressure and can slow down an app |
| Deep recursion | Each recursive call adds a stack frame — too many levels causes `StackOverflowException` |
| Struct vs class design choice | Small, immutable, short-lived data → `struct` (stack, cheap); complex/large/shared data → `class` (heap) |
| Memory leaks (indirect) | Heap objects aren't leaked in the traditional sense in C#, but holding unnecessary references (e.g., static events) prevents GC from collecting them |

## 6. Quick Summary Table

| | Stack | Heap |
|---|---|---|
| Lifetime | Tied to method/scope | Tied to reachability (GC-managed) |
| Speed | Fast | Slower |
| Managed by | CPU (automatic push/pop) | Garbage Collector |
| Typical contents | Value types, references, method frames | Objects, arrays, strings, boxed values |

