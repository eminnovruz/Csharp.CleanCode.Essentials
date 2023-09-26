<a href="top"></a> 
# C# , Clean Code Essentials

A brief information of writing clean code instead.

    


## Authors

- [@Emin Novruz](https://github.com/eminnovruz) 😺

## Project Repo Link
- [Csharp.CleanCode.Essentials](https://github.com/eminnovruz/Csharp.CleanCode.Essentials) 🔗



## Badges

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)

## What is spaghetti  code?
Spaghetti code, also known as spaghetti programming, is a term used to describe a programming style or a piece of code that is overly complex, tangled, and difficult to understand or maintain. It typically refers to code that lacks structure, has convoluted control flow, and is often characterized by a dense web of interconnected logic and branching.

- Unstructured Flow: Spaghetti code lacks a clear and organized structure. It may have excessive branching, loops, and conditional statements that are difficult to follow.

- Goto Statements: Historically, spaghetti code was often associated with the excessive use of "goto" statements, which allow code execution to jump to arbitrary points in the program. This leads to chaotic control flow.

- Poor Modularity: Spaghetti code tends to be monolithic, with little or no separation of concerns into functions or modules. This makes it challenging to reuse code and challenging to test.

- Lack of Documentation: Spaghetti code often lacks meaningful comments and documentation, making it even more challenging to understand.

- High Complexity: Due to its tangled nature, spaghetti code tends to have high complexity, making it prone to bugs and errors.

- Maintenance Nightmare: Spaghetti code is challenging to maintain over time. As the codebase grows, making changes or adding new features becomes increasingly risky and error-prone.

- Debugging Difficulty: Finding and fixing bugs in spaghetti code can be a time-consuming and frustrating process, as changes in one part of the code can unintentionally affect other parts.

- Refactoring Challenges: Refactoring spaghetti code to make it more structured and maintainable can be a daunting task, often requiring a significant rewrite.

- Modern Practices: Modern programming languages and best practices discourage the use of "goto" statements and emphasize structured programming, modularity, and clean code principles to avoid spaghetti code.

## Some tips for changing sphagetti code into clean code.
## Meaningful Names 👍.
### Use descriptive and meaningful names for variables, functions, classes, and modules.

```csharp
// Wrong Example
int a = 5; // What is "a" ?

// Correct Example
int numberOfBooks = 10; // So easy to understand what does it represents.
```

## Adding Some Comments 💬
### Add comments if it is necessary or should be explained.

```csharp
// Bad example
int a = Sum(5, 10); // Sum of 2 integer

// Correct example
int numberOne = 5;
int numberTwo = 10;
int result = Sum(numberOne, numberTwo); // Counting 2 number for specific purpose. 
```
### Write 'Summary' for methods.

```csharp
/// <summary> 
/// The function for adding new student. 
/// </summary>
/// <param name="newStudent">Student, will be added to list of students.</param>
public void AddStudent(Student newStudent)
{
    if (newStudent != null)
    {
        Students.Add(newStudent);
    }
    else
    {
        throw new ArgumentNullException(nameof(newStudent));
    }
}
```

## Formatting 📖
### Follow readable style of code.

```csharp

if (newStudent != null)
{
Students.Add(newStudent);  // Bad Example
}
else
{
    throw new ArgumentNullException(nameof(newStudent)); // Correct One
}

```

## Exception Handling ⚒️
### Handle Exceptions.

```csharp
List<Student> Students = null;

Students.Add(new Student("Kamil", 15, 9)); // Example will be finished with exception

// Correct example
try
{
    Student newStudent = new Student("Kamil", 15, 9);
    Students.Add(newStudent);
}
catch (Exception exception)
{
    Console.WriteLine(exception.Message);
}
```

## Dont repeat yourself (DRY) 🔁
### Try not to write same codes again and again.

```csharp
// Bad example
int result1 = CalculateSquare(5);
int result2 = CalculateSquare(10);

// Good example
int result1 = CalculateSquare(5);
int result2 = CalculateSquare(10);

int CalculateSquare(int x) {
    return x * x;
}
```
## Functions 🧩
- Try not to write complex functions.
- Keep functions focused on one thing.

```csharp 
// Code , full of errors and mistakes.
public void CountAndSave(int a, int b, FileStream s)
{
    int z = a + b;
    byte t = Byte.Parse(z.ToString());
    s.Write(t);
    Console.WriteLine("Saved!");
}

// Functions which are focused for one job.
public int Count(int numberOne, int numberTwo)
{
    // Some Codes here...
}

public void SaveNumber(FileStream stream, int number)
{
    // Some Codes again..
}
```
## Version Control 🛂

```bash
# Commit your changes with meaningful messages
git commit -m "Add CalculateSquare function"
git commit -m "Fix issue #123: Invalid input handling"

```

## Follow Solid Principles ⚡.
### There are 5 principles of Solid.

## Single Responsibility Principle.
### A class should have only one reason to change, meaning it should have only one responsibility.

```csharp 
// Bad example (violating SRP)
public class Student {
    public void CalculateGPA() { /* ... */ }
    public void SaveToDatabase() { /* ... */ }
}

// Good example (adhering to SRP)
public class Student {
    public double CalculateGPA() { /* ... */ }
}

public class StudentRepository {
    public void SaveToDatabase(Student student) { /* ... */ }
}

```

## Open/Closed Principle.
### Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification.

```csharp
// Bad example (violating OCP)
public class Rectangle {
    public double Width { get; set; }
    public double Height { get; set; }
}

// Extending for a new shape
public class Circle : Rectangle {
    public double Radius { get; set; }
}

// Good example (adhering to OCP)
public interface IShape {
    double Area();
}

public class Rectangle : IShape {
    public double Width { get; set; }
    public double Height { get; set; }
    
    public double Area() {
        return Width * Height;
    }
}

public class Circle : IShape {
    public double Radius { get; set; }
    
    public double Area() {
        return Math.PI * Math.Pow(Radius, 2);
    }
}

```
## Liskov Substitution Principle (LSP):
### Subtypes must be substitutable for their base types without altering the correctness of the program.

```csharp
// Bad example (violating LSP)
public class Bird {
    public virtual void Fly() { /* ... */ }
}

public class Ostrich : Bird {
    public override void Fly() {
        throw new NotSupportedException("Ostriches can't fly.");
    }
}

// Good example (adhering to LSP)
public interface IFlyable {
    void Fly();
}

public class Sparrow : IFlyable {
    public void Fly() { /* ... */ }
}

public class Ostrich : IFlyable {
    public void Fly() {
        throw new NotSupportedException("Ostriches can't fly.");
    }
}
```

## Interface Segregation Principle (ISP):
### Clients should not be forced to depend on interfaces they do not use.

```csharp
// Bad example (violating ISP)
public interface IWorker {
    void Work();
    void Eat();
}

public class Manager : IWorker {
    public void Work() { /* ... */ }
    public void Eat() { /* ... */ }
}

// Good example (adhering to ISP)
public interface IWorker {
    void Work();
}

public interface IEater {
    void Eat();
}

public class Manager : IWorker, IEater {
    public void Work() { /* ... */ }
    public void Eat() { /* ... */ }
}

```

## Dependency Inversion Principle (DIP):
### High-level modules should not depend on low-level modules. 
```csharp
// Bad example (violating DIP)
public class LightBulb {
    public void TurnOn() { /* ... */ }
    public void TurnOff() { /* ... */ }
}

public class Switch {
    private LightBulb bulb = new LightBulb();

    public void Toggle() {
        // Direct dependency on LightBulb
        if (bulb.IsOn()) {
            bulb.TurnOff();
        } else {
            bulb.TurnOn();
        }
    }
}

// Good example (adhering to DIP)
public interface ISwitchable {
    void TurnOn();
    void TurnOff();
}

public class LightBulb : ISwitchable {
    public void TurnOn() { /* ... */ }
    public void TurnOff() { /* ... */ }
}

public class Switch {
    private ISwitchable device;

    public Switch(ISwitchable device) {
        this.device = device;
    }

    public void Toggle() {
        if (device.IsOn()) {
            device.TurnOff();
        } else {
            device.TurnOn();
        }
    }
}

```

# Keep in Mind ⚠️
    This is not that all about writing clean code. You can get more information and tips from anywhere else.





![Logo](https://i0.wp.com/blog.knoldus.com/wp-content/uploads/2020/09/CleanCode.jpg?w=800&ssl=1)    

    I have got asists of both OpenAi and Forums for writing this article⚡.


[Back To Top](#top)








