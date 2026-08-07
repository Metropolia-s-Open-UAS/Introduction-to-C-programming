#### Command line arguments
- Until now we have omitted the command line parameters. You can often see the Main method defined as follows:
```c#
static int Main (String[] args)
```
OR
```c#
static void Main (String[] args)
```
- [ ] Here the parameter of the Main method is a `string array`, which holds the command line arguments if any are given.
- [ ] The parameter is optional.
- [ ] he parameter is optional. You can access the command line arguments from the args variable (*).
- [ ] The first command line argument is stored in the first element of the array, which can be accessed from `args[0]`.
- [ ] Second command line argument is available from `args[1]` and so on. The handling of command line argument is shown in the following example:
```C#
using System;
class CommandLineArgument{
 static void Main(string[], args){
  Console.Write("The first command line was :");
  Console.WriteLine(args[0]);
 }
}
```
> The reader should note that in the example, the program expects that the command line argument is always provided. In case the argument is not available, the program would exit with an unhandled exception. We will cover these topics later in the course.

> (*) You can get the args array length by accessing properties: `$length = args.Length;`


| Concept | Code / Syntax | Description | Key Notes |
| :--- | :--- | :--- | :--- |
| **Main with parameters** | `static void Main(String[] args)` <br> or <br> `static int Main(String[] args)` | The `Main` method can accept an array of strings (`String[]`) containing arguments passed when the program is launched. | The parameter name `args` is conventional but not mandatory (e.g., you could name it `arguments`). |
| **Return type: `void` vs `int`** | `void` → no return value <br> `int` → returns an exit code to the operating system | Returning an `int` allows you to signal success (`0` usually) or an error code (non-zero) to the calling process or script. | If you return `int`, you must include a `return` statement (e.g., `return 0;`). |
| **Parameter is optional** | You can omit `(String[] args)` entirely—as you did in your first program. | If your program doesn't need command-line inputs, you can leave the parameter out. The compiler accepts both signatures as valid entry points. | Overloading `Main` with and without parameters is *not* allowed as an entry point—only one `Main` method can exist as the entry point. |
| **Accessing arguments** | `args[0]` → first argument <br> `args[1]` → second argument, etc. | Command-line arguments are **zero-indexed**. The first argument after the program name is at index `0`. | There is **no** `args[0]` holding the program name (unlike C/C++). The executable name is *not* passed. |
| **Array properties** | `int count = args.Length;` | You can get the total number of arguments passed using the `Length` property. | This is crucial for checking how many arguments were provided before accessing them. |
| **Risk of exception** | Accessing `args[0]` when no argument is given throws an `IndexOutOfRangeException`. | Your text correctly warns about this—it will cause the program to crash with an unhandled exception. | **Best practice**: Always check `args.Length > 0` before accessing indices. |


| Point | Explanation |
| :--- | :--- |
| **Return type `int` is optional** | Returning `int` is useful when your program is called by another program (e.g., a batch script, CI/CD pipeline) that needs to know if the program succeeded or failed. `0` conventionally means success; any other number indicates an error. |
| **No program name in `args`** | Unlike C or C++, C# does **not** include the executable's path or name as the first element of `args`. If you pass `myApp.exe John 25`, then `args[0] = "John"` and `args[1] = "25"`. |
| **All arguments are strings** | Even if you pass numbers (e.g., `25`), they come in as strings. You must parse them (e.g., `int.Parse(args[1])`) if you need numeric values—with appropriate error handling. |
| **Spaces in arguments** | If an argument contains spaces (e.g., a full name), you must enclose it in **double quotes** when launching: `myApp.exe "John Doe" 25` → `args[0] = "John Doe"`, `args[1] = "25"`. |


```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        // Check if at least one argument was provided
        if (args.Length == 0)
        {
            Console.WriteLine("Error: No name provided!");
            Console.WriteLine("Usage: Program.exe <YourName>");
            return; // Exit early (for void Main)
            // Or: return 1; // if Main returns int
        }

        // Safely access the first argument
        string name = args[0];
        Console.WriteLine($"Hello, {name}!");
    }
}
```

**If you use `static int Main(string[] args)`:**  

```csharp
static int Main(string[] args)
{
    if (args.Length == 0)
    {
        Console.WriteLine("Error: No name provided.");
        return 1; // Non-zero exit code signals an error
    }

    Console.WriteLine($"Hello, {args[0]}!");
    return 0; // Success
}
```

| Environment | How to do it |
| :--- | :--- |
| **Visual Studio** | Go to **Project → Properties → Debug** → enter arguments in the "Command line arguments" field. |
| **VS Code / Terminal** | Navigate to the folder with your compiled `.exe` (or use `dotnet run`) and type: <br> `dotnet run -- John` <br> or <br> `MyApp.exe John` |
| **Windows Command Prompt** | `MyApp.exe John "Doe Smith" 25` |

