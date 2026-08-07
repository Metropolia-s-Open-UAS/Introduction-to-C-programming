#### Expressions and statements
- An **expression** is a combination of `variables`, `literals`, `method calls` and `operators` (`arithmetic` or `Boolean logical` operators) that can be evaluated to a single value. An **expression** must have one or more `operands` and `zero` or more operators. Operators are symbols that are used to perform operations on operands. We learn more about different kinds of operators in chapter 4.
> Examples of expressions:

> i + 1

> sum = a + b + c; // the right side of the statement (from equal sign) is an expression

> if (temp > 0 && temp <= 25) // expression evaluates to a Boolean value True
- A **statement** is an action that the program executes, and **does not return a result.** A statement can, for example, add three numbers together and store the result to a variable. Usually statements comprise of expressions and operators but not necessarily, like in the case of declarative statement.
> Examples of statements:
```csharp
Console.WriteLine(“Hello, World!”);
sum = a + b + c;
int i; // declarative statement
```

> **NOTE! If you hesitate in determining between an expression and a statement, here is a tip: if you can print it or assign it to a variable, it is an expression. If you cannot, it is a statement.**

| Concept | Definition | Key Characteristics | Does it return a value? | Examples |
| :--- | :--- | :--- | :--- | :--- |
| **Expression** | A combination of variables, literals, method calls, and operators that can be **evaluated to a single value**. | Must have at least one operand; may have zero or more operators. | **Yes**—always produces a result (e.g., `int`, `bool`, `string`). | `i + 1` <br> `a + b + c` <br> `temp > 0 && temp <= 25` <br> `args[0]` |
| **Statement** | An **action** that the program executes. It performs a task but does not return a result. | Can be composed of expressions, but doesn't have to be (e.g., declarations). | **No**—it performs an action and "ends" with a semicolon `;` or a block `{ }`. | `Console.WriteLine("Hi");` <br> `sum = a + b + c;` <br> `int i;` <br> `if (x > 0) { ... }` |


| Your Code | Type | Why? |
| :--- | :--- | :--- |
| `i + 1` | **Expression** | It evaluates to a numeric value (e.g., if `i` is 5, it becomes `6`). You could assign it: `int j = i + 1;`. |
| `a + b + c` (RHS of assignment) | **Expression** | The part *after* the equals sign evaluates to a single sum. It produces a value. |
| `temp > 0 && temp <= 25` | **Expression** | It evaluates to a Boolean (`true` or `false`). You could assign it: `bool isValid = temp > 0 && temp <= 25;`. |
| `Console.WriteLine("Hello, World!");` | **Statement** (specifically an *Expression Statement*) | The action is printing. `Console.WriteLine` returns `void` (nothing), so you *cannot* assign it to a variable. It cannot be used inside another expression. |
| `sum = a + b + c;` | **Statement** (Expression Statement) | The action is storing a value. The *entire line* does not return a value. However, the **right side** (`a+b+c`) is an expression. |
| `int i;` | **Statement** (Declaration Statement) | It declares a variable. It doesn't compute anything; it just reserves space in memory. |


- `"Hello"` → Can assign? Yes (`string x = "Hello";`). Can print? Yes (`Console.WriteLine("Hello")`). → **Expression**.
- `5 * 3` → Can assign? Yes (`int x = 5 * 3;`). → **Expression**.
- `Console.ReadLine()` → Can assign? Yes (`string input = Console.ReadLine();`). → **Expression** (it returns a `string`).
- `Console.WriteLine("Hi")` → Can assign? No (`var x = Console.WriteLine("Hi");` gives a compile error because it returns `void`). → **Statement** (the method call itself is a statement).

**The crucial nuance to add:** 
A single line of code can be **both**! Specifically, `Console.WriteLine("Hi");` is a **statement**. But if we look inside the parentheses, `"Hi"` is an **expression** (a string literal). 

Similarly, in `sum = a + b + c;`, the whole line is a **statement**, but:
- The `a + b + c` part is an **expression**.
- The `sum =` part is the **assignment operator** making it an action.

---


In C#, **assignments are actually expressions** too! Wait, let me clarify:

- In most cases, `x = 5;` is written as a **statement**.
- But syntactically, the assignment operator `=` returns the value that was assigned. This means you can chain assignments:

```csharp
int a, b, c;
a = b = c = 10; // This works!
```
Here, `c = 10` evaluates to `10`, then `b = 10` evaluates to `10`, then `a = 10`. So `c = 10` is an *expression* used inside a larger statement. This blurs the line—but for beginners, just remember: if it ends with a semicolon `;` and does an *action*, it's a statement.


| Look for this... | It is a... |
| :--- | :--- |
| Ends with a semicolon `;` or curly braces `{ }` | **Statement** (usually) |
| Can be placed on the right side of an equals sign `=` | **Expression** |
| Can be passed as an argument to a method (e.g., inside `Console.WriteLine(...)`) | **Expression** |
| Declares a variable (`int x;`, `string y;`) | **Statement** |
| Controls flow (`if`, `for`, `while`, `switch`) | **Statement** (Control Flow Statement) |


