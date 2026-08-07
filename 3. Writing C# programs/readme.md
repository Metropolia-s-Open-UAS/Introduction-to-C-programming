#### Basic structure of a C# Program
- In this chapter we start C# programming in practice.
- We begin from the fundamentals of writing programs by going through a simple program line-by-line and then study commenting, variables, expressions and statements in C#.

> The Hello World greeting is a traditional first program when learning a new programming language. In the below example, you can see the program written in C#. Note, that Visual Studio Community adds some informative items in the editor: line numbers, dashed and solid lines and boxes with minus signs are all extraneous and are not actually part of the source code.
```C#
using system
class HelloWorld
{
 static void Main()
   {
     console.WriteLine("Hello, World!");
   }
}
```

| Code Element | Syntax / Code | Line(s) | Description | Additional Notes |
| :--- | :--- | :--- | :--- | :--- |
| **Using Directive** | `using System;` | 1 | Tells the program to use the `System` namespace, allowing access to classes like `Console` without full qualification. | Every statement in C# must end with a semicolon (`;`). |
| **Class Definition** | `class HelloWorld { ... }` | 3–4 | Defines a new class named `HelloWorld`. The opening curly brace `{` marks the start of the class body. | The closing curly brace `}` (not shown in the snippet) marks the end. |
| **Entry Point Method** | `static void Main() { ... }` | 5–6 | Defines the `Main` method—the application's entry point, invoked automatically when the program starts. | - `static` → can be called without creating an object.<br>- `void` → returns nothing. The method body is enclosed in curly braces `{ }`. |
| **Console Output** | `Console.WriteLine("Hello, World!");` | 7 | Calls the `WriteLine` method of the `Console` class (from `System`) to print text to the console window. | The text goes inside double quotes and parentheses. |
| **Method Behavior (Extra Note)** | `WriteLine` vs `Write` | — | `WriteLine` automatically appends a newline terminator (`\r\n` on Windows) at the end of the output. | If you use `Console.Write`, you must manually add line breaks (e.g., `\r\n`) to terminate lines. |
