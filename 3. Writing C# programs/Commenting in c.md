
### Table: Commenting in C#

| Comment Type | Syntax | Scope / Behavior | Primary Use Case | Example |
| :--- | :--- | :--- | :--- | :--- |
| **Single-line** | `//` | Everything after `//` on that same line is ignored by the compiler. | Explaining a specific line of logic; temporarily disabling a single line of code during debugging. | `string name = args[0]; // Get the user's name from CLI` <br> <br> `// Console.WriteLine("Debugging line");` |
| **Multi-line (Block)** | `/*` to `*/` | Everything between the opening `/*` and closing `*/` is ignored. Can span multiple lines or just one. | Writing longer explanations (e.g., summarizing a complex algorithm); temporarily disabling a large block of code. | `/* This section validates the input. It checks for null, empty strings, and whitespace. */` <br> <br> `/* Console.WriteLine("Line 1");` <br> `   Console.WriteLine("Line 2"); */` |

| Topic | Explanation |
| :--- | :--- |
| **Compilation Behavior** | As you correctly stated, comments are **stripped out** during compilation. They do **not** affect the size or performance of your compiled `.exe` or `.dll`—they exist purely for the humans reading the code. |
| **Nesting Limitation** |  **Multi-line comments do NOT nest.** If you write `/* Outer /* Inner */ Outer */`, the compiler stops at the very first `*/` (ending at "Inner"). This can cause unexpected errors. **Single-line comments** are generally safer for commenting out code that already contains `/*` or `*/`. |
| **Temporary Code Disabling** | Using `//` at the start of a line is the fastest way to disable a single statement while debugging. For large blocks, highlight the code in your IDE (like VS or VS Code) and use the shortcut **Ctrl + K, Ctrl + C** (to comment) and **Ctrl + K, Ctrl + U** (to uncomment). |



Since you're building a strong foundation, it's worth mentioning that professional C# developers use a **third** type of comment: **XML Documentation Comments**.

- **Syntax:** Starts with **three forward slashes** (`///`).
- **Purpose:** These are *not* just for display—they generate an XML file that provides IntelliSense tooltips when other developers hover over your methods or classes in their IDE. They are also used by tools like **Sandcastle** to generate automatic API documentation (like Microsoft's official docs).

**Example:**
```csharp
/// <summary>
/// Greets the user with a personalized message.
/// </summary>
/// <param name="name">The name of the user to greet.</param>
/// <returns>A string containing the greeting.</returns>
static string GreetUser(string name)
{
    return $"Hello, {name}!";
}
```
