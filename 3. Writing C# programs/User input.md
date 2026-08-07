#### User input
- Now, let us explore another example. We keep the basic structure the same but introduce the use of a variable and user interaction. We omit the lines we explained in the earlier example.
```c#
using System;
class HelloStanger{
 static void Main(){
  string answer;
  console.write("Identify Yourself, Stranger");
  answer = Console.ReadLine();
  console.writeLine("Nice to meet you, "+ answer+"!");
 }
}
```

#### Table: User Input & Output with Variables

| Line | Code | Concept | Description | Key Syntax / Notes |
| :--- | :--- | :--- | :--- | :--- |
| **7** | `string answer;` | **Variable Declaration** | Declares a variable named `answer` that can store text (`string` type). At this point, it has no value (it is `null` for reference types). | Syntax: `type variableName;` <br> Variables store runtime data for later use (covered in Ch. 4). |
| **9** | `Console.Write("Identify yourself, stranger: ");` | **Prompt (No Newline)** | Prints a prompt to the console *without* moving to the next line. This keeps the cursor right after the colon, so the user types their answer on the same line. | Uses `Console.Write` instead of `WriteLine` to avoid a line break before input. |
| **10** | `answer = Console.ReadLine();` | **Input & Assignment** | Reads one full line of text from the user (until they press Enter) and stores it into the `answer` variable using the **assignment operator** (`=`). | `Console.ReadLine()` returns a `string`. The `=` operator assigns that returned value to `answer`. |
| **11** | `Console.WriteLine("Nice to meet you, " + answer + "!");` | **String Concatenation** | Combines (concatenates) the literal strings `"Nice to meet you, "` and `"!"` with the variable `answer` using the `+` operator, then prints the full result to the console. | You can mix hard-coded text and variables in any order. The entire expression inside the parentheses is evaluated *before* being printed. |


| Your Text | Should Be | Why |
| :--- | :--- | :--- |
| `ConsoleWrite(` | `Console.Write(` | The method is `Console.Write` (with a dot between `Console` and `Write`). |
| `ConsoleWriteLine(` | `Console.WriteLine(` | Same here—the dot is required. C# is case-sensitive and relies on the dot (`.`) operator to access methods inside a class. |

####  Additional Insights & Best Practices

1. **Input is always a string:**  
   `Console.ReadLine()` **always** returns a `string`. If you later need a number (e.g., an `int` or `double`), you must **parse** it—for example: `int age = int.Parse(Console.ReadLine());` (with error handling using `TryParse` in real projects).

2. **String Interpolation (A cleaner alternative):**  
   While concatenation (`+`) works perfectly, C# offers a more readable way: **string interpolation** using the `$` symbol.  
   Instead of:  
   `Console.WriteLine("Nice to meet you, " + answer + "!");`  
   You can write:  
   `Console.WriteLine($"Nice to meet you, {answer}!");`  
   This embeds the variable directly inside the string within curly braces `{}`—much cleaner for longer outputs!

3. **What happens if the user just presses Enter?**  
   `Console.ReadLine()` will return an **empty string** (`""`), not `null`. If the user presses Ctrl+Z, it returns `null`. In real applications, you'd check for this to avoid unexpected behavior.

4. **The assignment operator (`=`) vs. equality (`==`):**  
   In Line 10, `=` is used for *assignment*—it stores the right-side value into the left-side variable. Don't confuse this with `==`, which is used for *comparison* (checking if two values are equal). You'll cover this in Ch. 4!

