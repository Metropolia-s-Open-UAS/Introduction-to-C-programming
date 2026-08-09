#### Loops in C#

#### 1. Loop Constructs Overview

| Loop Type | Syntax | Description | Best Used When |
|---|---|---|---|
| `for` | `for (init; cond; increment) { }` | Runs a fixed number of iterations with a counter | You know exactly how many times to loop |
| `while` | `while (cond) { }` | Checks condition **before** each iteration | Loop depends on a condition, may run 0 times |
| `do...while` | `do { } while (cond);` | Checks condition **after** each iteration | Loop must run **at least once** |
| `foreach` | `foreach (var item in collection) { }` | Iterates over each element of a collection | Iterating arrays, lists, or any `IEnumerable` |

#### 2. `for` Loop

| Component | Example | Notes |
|---|---|---|
| Initializer | `int i = 0` | Runs once, before the loop starts |
| Condition | `i < 10` | Checked before each iteration; loop stops when `false` |
| Iterator | `i++` | Runs after each iteration |
| Multiple variables | `for (int i=0, j=10; i<j; i++, j--)` | Comma-separated init/iterator expressions allowed |
| Infinite loop | `for ( ; ; ) { }` | All three parts optional; needs a `break` to exit |

```csharp
for (int i = 1; i <= 5; i++)
{
    Console.WriteLine(i);
}
```

#### 3. `while` Loop

| Feature | Example | Notes |
|---|---|---|
| Basic form | `while (count < 5) { count++; }` | Condition tested first — may not execute at all |
| Infinite loop | `while (true) { ... break; }` | Common pattern with an internal exit condition |

```csharp
int count = 0;
while (count < 5)
{
    Console.WriteLine(count);
    count++;
}
```

#### 4. `do...while` Loop

| Feature | Example | Notes |
|---|---|---|
| Basic form | `do { ... } while (cond);` | Body always executes **at least once** |
| Semicolon required | `} while (cond);` | Don't forget the trailing `;` |

```csharp
int num;
do
{
    Console.WriteLine("Enter a number (0 to stop): ");
    num = Convert.ToInt32(Console.ReadLine());
} while (num != 0);
```

#### 5. `foreach` Loop

| Feature | Example | Notes |
|---|---|---|
| Basic form | `foreach (int x in numbers) { }` | Read-only access to each element |
| With `var` | `foreach (var x in numbers) { }` | Type inferred automatically |
| Over a `Dictionary` | `foreach (var kvp in dict) { kvp.Key; kvp.Value; }` | Element type is `KeyValuePair<TKey,TValue>` |
| Cannot modify collection | — | Adding/removing items during iteration throws `InvalidOperationException` |

```csharp
int[] numbers = { 1, 2, 3, 4, 5 };
foreach (int n in numbers)
{
    Console.WriteLine(n);
}
```

#### 6. Loop Control Keywords

| Keyword | Effect | Example |
|---|---|---|
| `break` | Exits the loop immediately | `if (i == 5) break;` |
| `continue` | Skips rest of current iteration, moves to next | `if (i % 2 == 0) continue;` |
| `goto` (rare) | Jumps to a labeled statement | `goto End;` |
| Nested loop `break` | Only exits the **innermost** loop | Use a labeled `break` alternative (flag variable) for outer loop |

#### 7. Quick Comparison — When to Use What

| Scenario | Recommended Loop |
|---|---|
| Known number of iterations | `for` |
| Unknown iterations, condition-based, may run 0 times | `while` |
| Must run at least once (e.g., menu prompts) | `do...while` |
| Iterating over arrays/lists/collections | `foreach` |
| Need index access while iterating | `for` |
| Just need each value, no index needed | `foreach` |

#### Loop Performance Characteristics: `for` vs `foreach`

#### 1. Performance Comparison

| Aspect | `for` | `foreach` |
|---|---|---|
| Arrays | Fastest — direct index access, JIT can eliminate bounds checks | Very fast too — compiler optimizes arrays specially, nearly identical to `for` |
| `List<T>` | Fast — uses indexer `list[i]` | Slightly slower — uses `IEnumerator`, allocates an enumerator (struct, usually no heap allocation) |
| `IEnumerable<T>` (generic interfaces, LINQ results) | Not directly usable (no indexer) | Only real option — but enumerator may be a class, causing heap allocation/boxing |
| `Dictionary<TKey,TValue>` | Not usable (no indexer) | Required — iterates `KeyValuePair<TKey,TValue>` |
| Bounds/index safety | Manual — risk of off-by-one errors | Automatic — no manual index management |
| Readability | More verbose | Cleaner, more declarative |

#### 2. Why the Differences Exist

| Reason | Explanation |
|---|---|
| Array special-casing | The C# compiler emits a `for`-like loop under the hood for `foreach` over arrays (`T[]`), so performance is nearly identical to a manual `for` |
| `List<T>` uses a struct enumerator | `List<T>.Enumerator` is a `struct`, so `foreach` avoids heap allocation — but the `MoveNext()`/`Current` call overhead is still slightly more than raw indexer access |
| Interface-typed enumerables | If a collection is accessed through `IEnumerable<T>` (not the concrete type), the enumerator gets boxed to the interface, causing a heap allocation — this is the main real-world "foreach is slower" case |
| `for` needs an indexer | Only works on types implementing `this[int index]` (arrays, `List<T>`, `String`) — can't be used on `Dictionary`, `HashSet`, `Queue`, etc. |

#### 3. Practical Guidance

| Situation | Recommendation |
|---|---|
| Iterating a plain array (`int[]`, `string[]`) | Either works — performance is essentially the same |
| Iterating `List<T>` in a hot loop (called millions of times) | `for` with indexer is marginally faster if every microsecond counts |
| Iterating `List<T>` in typical application code | `foreach` — negligible difference, more readable |
| Iterating `Dictionary`, `HashSet`, `Queue`, `Stack` | `foreach` — no indexer exists, so it's your only clean option |
| Iterating and modifying the collection at the same time | `for` (with care) — `foreach` throws `InvalidOperationException` if the collection changes during iteration |
| Working with LINQ query results | `foreach` — LINQ returns `IEnumerable<T>`, no indexer available |
| Need the current index value inside the loop | `for` — `foreach` doesn't expose an index (you'd need a separate counter variable) |

#### 4. Example: Same Task, Both Ways

```csharp
List<int> numbers = new List<int> { 10, 20, 30, 40, 50 };

// for — index access, can also modify list by position
for (int i = 0; i < numbers.Count; i++)
{
    Console.WriteLine("Index " + i + ": " + numbers[i]);
}

// foreach — cleaner, but no index unless you track it yourself
int idx = 0;
foreach (int n in numbers)
{
    Console.WriteLine("Index " + idx + ": " + n);
    idx++;
}
```
