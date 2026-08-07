#### Creating a Project in Visual Studio Community
- To create a new project in Visual Studio, choose “Create a new project” when the software starts. If you have projects that you have worked on earlier, they will be presented on the left column (Open recent). In the below image you can see the start-up screen after the installation is presented.
- After clicking the "Create a new project" button you will be shown a screen to choose a project template. Find and choose Console App (.NET Framework) as shown in the next image.

#### Building a solution
- Let us create a simple solution. Add the two lines of code as shown in the image. As we will learn in the next chapter, line 13 prints the text "Hello, World!" on the screen. Line 14 requests the user to input a key - the purpose of this will be demonstrated shortly.

- After the modifications, save the program from File/Save and choose Build/Build Solution. You should see a message "Build Succeeded" on the bottom of the Visual Studio window. Now push the Start button and Visual Studio should run the program.
- Let us now make some observations about the program. Firstly, we left the default Visual Studio Using-directives intact. The examples on this course in most cases do not include other than the root System directive. Secondly, we simplify the code structure by leaving out the namespace. Finally, if the solution is only including printing on the screen add the Console.ReadKey() in a suitable place to prevent the execution window disappearing from the Visual Studio.

> NOTE! When returning the solution to Viope, remove any ReadKey() calls! An alternative method is to open a command prompt in Windows and navigate to the build directory (e.g. C:\Users\John\source\repos\HelloWorld\bin\Debug) and use the executable directly.





