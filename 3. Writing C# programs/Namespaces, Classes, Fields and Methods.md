#### Namespaces, Classes, Fields and Methods
##### Namespaces
- Namespaces are heavily used in object-oriented languages, also in C#.
- Namespaces group related code like classes, interfaces, enums and structs.
- In our first program we used `.NET` System namespace, which allowed us to use an existing method for output.
> By using namespaces we can avoid naming conflicts. You can read more about .NET namespaces using Microsoft’s dotnet documentation for the .NET Framework, available online.

##### Classes, Fields and Methods
- C# is an object-oriented programming language.
- Everything in the C# programming language is associated with classes, objects, fields and methods.
- A class can be thought as a blueprint for creating objects, which interact within the program.
- In our first example we used the Console class and `WriteLine `method belonging to it.
> Classes (or objects) store information in fields (class variables) and define functionalities in methods. We learn more about object-oriented programming and in chapter 9.

| Concept | Definition | How it appears in "Hello, World!" | Real-world analogy |
| :--- | :--- | :--- | :--- |
| **Namespace** | A container that groups related code (classes, interfaces, enums, structs) to avoid naming conflicts. | `using System;` allows us to type `Console` instead of the fully qualified `System.Console`. | A **folder** on your computer that organizes related files. You can have a "Drawing" folder and a "Music" folder, both containing a file named `Notes.cs` without conflict. |
| **Class** | A blueprint or template for creating objects. It defines what data (fields) and actions (methods) the objects will have. | `class HelloWorld { ... }` defines our program's main blueprint. `Console` is also a predefined class in the `System` namespace. | An **architect's blueprint** for a house. The blueprint itself isn't a house, but it defines what every house built from it will have. |
| **Field** | A variable declared inside a class that stores data (state) for that class or its objects. | *Not explicitly present in this simple program*, but for example, a `Person` class might have fields like `string name;` or `int age;`. | The **attributes** of the blueprint—like the number of bedrooms or the type of foundation. |
| **Method** | A block of code inside a class that performs a specific action or defines a behavior. | `static void Main()` is a method (the entry point). `Console.WriteLine()` is a method (provided by .NET) that performs the action of printing text. | The **actions** a house can have—like "openGarageDoor()" or "turnOnHeating()". |

---

### A few extra clarifications based on your text:

- **Why `using System;` matters:** Without it, you would have to write `System.Console.WriteLine("Hello, World!");` every single time. The `using` directive is just a convenience shortcut—it doesn't "import" code; it tells the compiler, *"When you see `Console`, look inside the `System` namespace for it."*
- **Static vs. Instance:** You correctly noted that `Main` is `static`. Notice that `Console.WriteLine()` is also called *without* creating a `Console` object (e.g., `new Console()`). That means `WriteLine` is a **static method** too. In later chapters, you'll learn about **instance methods**, which require you to create an object first (e.g., `Person p = new Person(); p.SayHello();`).
- **Fields in the future:** Once you start creating your own classes (like a `Car` or `Student` class), you'll add fields to store data. Those fields will usually be marked as `private` to protect them, and you'll access them via methods or properties—a core principle of encapsulation in OOP.
