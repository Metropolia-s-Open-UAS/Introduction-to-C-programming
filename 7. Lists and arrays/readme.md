#### Arrays and Lists in C#


| Feature | Array | `List<T>` |
|---|---|---|
| Namespace | Built-in (no `using` needed) | `System.Collections.Generic` |
| Size | Fixed at creation | Dynamic — grows/shrinks automatically |
| Declaration | `int[] arr = new int[5];` | `List<int> list = new List<int>();` |
| Add elements | Not possible after creation | `list.Add(5);` |
| Remove elements | Not possible | `list.Remove(5);` / `list.RemoveAt(index);` |
| Access by index | `arr[0]` | `list[0]` |
| Performance | Slightly faster (no overhead) | Slightly slower (dynamic resizing overhead) |
| Type safety | Strongly typed | Strongly typed (generic) |
| When to use | Fixed-size, performance-critical data | Size unknown or changes at runtime |


| Method | Syntax | Notes |
|---|---|---|
| Declare with size | `int[] numbers = new int[5];` | Creates array of 5 elements, all default (`0` for int) |
| Declare with values | `int[] numbers = { 1, 2, 3, 4, 5 };` | Size inferred from initializer list |
| Declare with `new` and values | `int[] numbers = new int[] { 1, 2, 3 };` | Explicit form, same result |
| Multi-dimensional | `int[,] grid = new int[3,3];` | Rectangular array (fixed rows/cols) |
| Jagged array | `int[][] jagged = new int[3][];` | Array of arrays, each row can have different length |
| String array | `string[] names = { "Amir", "Sara" };` | Same syntax, any type works |

```csharp
int[] scores = { 90, 85, 77, 92 };
Console.WriteLine(scores[0]);    // 90
Console.WriteLine(scores.Length); // 4
```


| Operation | Syntax | Notes |
|---|---|---|
| Length | `arr.Length` | Property, not method (no parentheses) |
| Loop through | `foreach (int x in arr)` or `for (int i=0; i<arr.Length; i++)` | Both common |
| Sort | `Array.Sort(arr);` | Sorts in place, ascending |
| Reverse | `Array.Reverse(arr);` | Reverses in place |
| Find index | `Array.IndexOf(arr, value);` | Returns -1 if not found |
| Copy | `Array.Copy(source, dest, length);` | Or `arr.Clone()` for a full copy |
| Clear (reset values) | `Array.Clear(arr, 0, arr.Length);` | Resets elements to default values |


| Method | Syntax | Notes |
|---|---|---|
| Empty list | `List<int> nums = new List<int>();` | Starts with 0 elements |
| With initial values | `List<int> nums = new List<int> { 1, 2, 3 };` | Collection initializer syntax |
| From an array | `List<int> nums = new List<int>(myArray);` | Converts array to list |
| With initial capacity | `List<int> nums = new List<int>(100);` | Pre-allocates internal storage (optimization, not a fixed size) |

```csharp
List<string> fruits = new List<string> { "Apple", "Banana" };
fruits.Add("Cherry");
Console.WriteLine(fruits.Count); // 3
```


| Operation | Syntax | Notes |
|---|---|---|
| Count elements | `list.Count` | Property (like `Length` for arrays) |
| Add | `list.Add(item);` | Appends to end |
| Add multiple | `list.AddRange(otherList);` | Appends a whole collection |
| Insert at position | `list.Insert(2, item);` | Inserts at specific index |
| Remove by value | `list.Remove(item);` | Removes first matching occurrence |
| Remove by index | `list.RemoveAt(2);` | Removes element at index |
| Remove all matching | `list.RemoveAll(x => x > 10);` | Takes a predicate (lambda) |
| Contains | `list.Contains(item);` | Returns `bool` |
| Find index | `list.IndexOf(item);` | Returns -1 if not found |
| Sort | `list.Sort();` | In place, ascending |
| Reverse | `list.Reverse();` | In place |
| Clear all | `list.Clear();` | Empties the list (`Count` becomes 0) |
| Convert to array | `list.ToArray();` | Returns a fixed-size array copy |


| Scenario | Example |
|---|---|
| Array of objects | `Person[] people = new Person[3];` |
| List of objects | `List<Person> people = new List<Person>();` |
| Adding a custom object | `people.Add(new Person("Ali", 25));` |
| Accessing properties | `people[0].Name` |

```csharp
class Person
{
    public string Name;
    public int Age;
    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }
}

List<Person> people = new List<Person>();
people.Add(new Person("Amir", 30));
people.Add(new Person("Layla", 25));

foreach (Person p in people)
{
    Console.WriteLine(p.Name + " is " + p.Age);
}

| Situation | Use |
|---|---|
| Fixed number of items known in advance, performance matters | `Array` |
| Number of items unknown or changes over time | `List<T>` |
| Need to frequently Add/Remove items | `List<T>` |
| Working with multi-dimensional data (grids, matrices) | `Array` (`[,]` or `[][]`) |
| Need built-in helper methods (`Find`, `Sort`, `RemoveAll` with lambdas) | `List<T>` |
| Passing fixed-size data to older APIs/methods expecting `T[]` | `Array` (or `list.ToArray()`) |

