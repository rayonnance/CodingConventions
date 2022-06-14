# **Coding Convention**

As many developers works on Rayonnance Products projects, we need to keep a coding syntax coherence in order to maintain the code **easy to ready and modify by any developers**.

This page list the principals coding convention that we **must follow for any new development**.

Some legacy part of the code didn’t respect theses rules for some history reasons. But we must follow the coding convention for any new code even in legacy classes.

-----

- [**Coding Convention**](#coding-convention)
  - [**What is a good code?**](#what-is-a-good-code)
  - [**Sources**](#sources)
  - [**Global Conventions**](#global-conventions)
  - [**C# Coding Conventions**](#c-coding-conventions)
    - [**Style**](#style)
  - [1. Class elements must be ordered as](#1-class-elements-must-be-ordered-as)
  - [2. Within each of these groups order by access](#2-within-each-of-these-groups-order-by-access)
  - [3. Within each of the access groups, order by](#3-within-each-of-the-access-groups-order-by)
  - [Long instruction spliting and code block use only one indentation](#long-instruction-spliting-and-code-block-use-only-one-indentation)
  - [Naming](#naming)
    - [**Syntax**](#syntax)
    - [**Error management**](#error-management)
    - [**Internationalization**](#internationalization)
    - [**Comment**](#comment)
    - [**Architecture**](#architecture)
    - [**Performances**](#performances)

## **What is a good code?**

Generally we define a good code as a code that implementing rules in a specific programming language without bug (e.g. non cover edge cases) and providing good performance.

After this assumption, we have to ensure the code can be maintain by developers over the time for bug fixing, implementing new features, resolve technical dept...

In consequence, **the code we write must be readable by any developers** **without external explanations or documentations**.

This assumption must be present in head of any developers from the first line of code to the last one.

In order to help developers to write readable code, we need to define common coding conventions that everybody respect. This is the aim of this page and will be detail in newt chapters.

## **Sources**

This documentation is based on Microsoft Coding Conventions with some minor modification and extra details for C# parts.

We can find original C# Coding Conventions at:

- <https://github.com/dotnet/runtime/blob/main/docs/coding-guidelines/coding-style.md>
- <https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions>
- <https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/>
- <https://github.com/DotNetAnalyzers/StyleCopAnalyzers/blob/master/DOCUMENTATION.md>

## **Global Conventions**

- All code and documentation must be written in English US.
- All text file must be encoded in UTF8 with Windows line-endings (in case of exception, it must be specified at the beginning of the file)
- Use four spaces indentation (no tabs)
- Avoid more than one empty line at any time. For example, do not have two blank lines between members of a type.
- Avoid unnecessary extra spaces characters. Example: avoid if (someVar == 0)···, where the “·" are spaces characters.

## **C# Coding Conventions**

### **Style**

- Use [Allman style](http://en.wikipedia.org/wiki/Indent_style#Allman_style) braces, where each brace begins on a new line then follow by an indentation:

```csharp
while (x == y)
{
     something();
}
```

- When using a single-statement if(), follow these conventions:
  
  ❌Never use single-line form like:

  ````csharp
  if (source == null) throw new ArgumentNullException("source");
  ````

  ❎ Using braces is always accepted, and required if any block of an if/else if/.../else compound statement uses braces or if a single statement body spans multiple lines:

  ````csharp
  if (...)
  {
      ...
  }
  else 
  {
      ...
  }
  ````

  ❎ Braces may be omitted only if the body of the block associated with an if() is placed on a single line:

  ````csharp
  if (source == null)
      throw new ArgumentNullException("source");
  ````

## 1. Class elements must be ordered as

1. Constant Fields
2. Fields
3. Delegates / Events
4. Enums
5. Properties
6. Constructors / Finalizers (Destructors)
7. Methods
8. Structs / Inner Classes

## 2. Within each of these groups order by access

1. Public
2. Internal
3. Protected internal
4. Protected
5. Private

## 3. Within each of the access groups, order by

1. Static
2. Non-static

## Long instruction spliting and code block use only one indentation

````csharp
❌
public void myMethod(
                  string param1,
                  string param2)
{
    var test = myOtherMethod(
                              param1,
                              param2);
}
````

````csharp
❎
public void myMethod(
    string param1,
    string param2)
{
    var test = myOtherMethod(
    param1,
    param2);
}
````

## Naming

Naming is a very important and difficult thing in programming. We need to choose a meaningful and easily readable name. 

We have to put yourself in someone else's shoes in order to see how the name could be interpreted by someone else. 

Also we need to define a common vocabulary that will used across the application code and avoid different name for a same concept or object.

- Favor readability over brevity.
- Use PascalCasing when naming a assembly, namespace, class, record or struct.
  - But when naming an interface, use PascalCasing in addition to prefixing the name with an I. This clearly indicates to consumers that it's an interface:

````csharp
public interface IWorkerQueue
{ ... }
````

- Use PascalCasing when naming public members types, such as fields, properties, events, methods, and local functions.
  - But when naming fields with internal or private visibility, use camelCase (and use readonly where possible).
- When using readonly static fields, readonly should come after static (e.g. static readonly not readonly static).
- Use camelCase for methods parameters names.
- Use UPPER\_CASE for constant fields names.
- Classes and structs names must be a nouns or noun phrases. Example: public class DataService
- Properties names must be a noun phrase or adjective. Example: public Color Color { get; set; }
- Boolean fields and methods returning a boolean must be named at interrogative form and start by Is, Are, or Can. Example: CanScrollHorizontally
  - And must be on the positive form. Example: ![(error)](Aspose.Words.136197ad-a876-40f5-8dfc-d2499b691605.001.png) CanNotSeek ![(tick)](Aspose.Words.136197ad-a876-40f5-8dfc-d2499b691605.001.png) CanSeek
- Methods names must be verbs or verb phrases. Example: public int CompareTo(...)
### **Syntax**
- Avoid this. unless absolutely necessary.
- Use var when the type is explicitly named on the right-hand side, typically due to either new or an explicit cast, e.g. var stream = new FileStream(...) not var stream = OpenStandardInput().
- Use language keywords instead of BCL types (e.g. int, string, float instead of Int32, String, Single, etc) for both type references as well as method calls (e.g. int.Parse instead of Int32.Parse).
- Always specify the visibility, even if it's the default (e.g. private string \_foo not string \_foo). Visibility should be the first modifier (e.g. public abstract not abstract public).
- Namespace imports should be specified at the top of the file, *outside* of namespace declarations, and should be sorted alphabetically, with the exception of System.\* namespaces, which are to be placed on top of all others.
- Avoid as is possible negative if() conditional test form like if(!string.IsEmpty()). Alternatives solutions can be:
  - Try to invert the code logic to get positive if() tests.
  - Use early return pattern to return at the beginning of the method if data need is not present:

````csharp
public string Sanitize(string url)
{
    if (string.IsNullOrEmpty(url))
        return;  
    [...]
}
````

- If previous mechanism cannot be apply, use a custom string extension with a positive expression:

````csharp
if (string.HasAny(url))
````

- Never let optional parameters without a default value. This help developers to understand witch parameters are optional only with method signature. Example:

````csharp
public string Join(string[] elements, string separator = null)
{ ... }
````

- Always call the Dispose() method of IDisposable objects. Try as possible to declare the disposable object in using() statement (Dispose() will be called automatically). Example:

````csharp
using (Font font = new Font("Arial", 10.0f))
{
    byte charset = font.GdiCharSet;
}
````

- Strings:
  - Use nameof(...) instead of "..." whenever possible and relevant.
  - Use [string interpolation](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/interpolated) to concatenate short strings, as shown in the following code:

string displayName = $"{nameList[n].LastName}, {nameList[n].FirstName}";

- To append strings in loops, especially when you're working with large amounts of text, use a [StringBuilder](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder) object:

````csharp
var phrase = "StringConcatainationCanBeIOExhaustiveBecauseItOverwriteAllTheString";
var manyPhrases = new StringBuilder();
for (var i = 0; i < 10000; i++)
{
    manyPhrases.Append(phrase);
}
````

### **Error management**
Exception is a great mechanism to manage error in code but it’s also recourse exhaustive and must be used carefully.

Throwing an exception should be use only when the member cannot do what it was designed to do (what the member name implies). In consequence, method should not return error code because exceptions are the primary means of reporting errors.

- Do not use exceptions for the normal flow of control but only for error management.
- Generic exception type can be used use:
  - ![(error)](Aspose.Words.136197ad-a876-40f5-8dfc-d2499b691605.001.png) Do not throw System.Exception, System.SystemException, ApplicationException, NullReferenceException types.
  - ![(tick)](Aspose.Words.136197ad-a876-40f5-8dfc-d2499b691605.001.png) Use InvalidOperationException if the object is in an inappropriate state.
  - Use ArgumentException or one of its sub-types if bad arguments are passed to a member (and set the ParamName property).
  - Implement your own dedicated exception type inherited from System.Exception.
- Exception that are throws then catches by our code should be a dedicated exception type in order to allow developer to implement dedicated error management code in catch block. Example:

````csharp
public Cron Parse(string cronString)
{
    if (!isValid(cronString))
    {
      // This custom exception type could be catched by the caller 
      // and allow to implement dedicated behavior
      // (like display error message to the user)
      throw new WrongCronFormatException();
    }
...
````

- Catching exception:
  - Do not catch exception without an action in catch block or at least an error log.
  - If you need to re-throw an exception, use throw; to preserve the original stack trace. Example:

````csharp
catch (DivideByZeroException ex)
{
    Console.WriteLine("Can't divide by 0");
    throw;
}
````

- Some error-free approaches:
  - Always instantiate all object members in class constructor.
  - Use TryParse() implementation if available instead of Parse().
  - Check public method parameters before using them (defensive programming).
### **Internationalization** 
- All labels must be translated in French and English US in resources.
- Use DateTime.UtcNow instead of DateTime.Now to avoid get time in current timezone. And use the ToLocalTime() DateTime property to display the time to current user time zone.
### **Comment**
- Place the comment on a separate line, not at the end of a line of code.
- Begin comment text with an uppercase letter.
- End comment text with a period.
- Insert one space between the comment delimiter (//) and the comment text, as shown in the following example:

// The following declaration creates a query. It does not run

// the query.

- Don't create formatted blocks of asterisks around comments.
- Ensure all public members have the necessary XML comments providing appropriate descriptions about their behavior.
- If a public method expose an interface, you should put the documentation on the interface and add /// <inheritdoc> to the public method implementation.
  - Exception: If the interface have multiple implementations, we can have dedicated documentation on methods.
### **Architecture**
- **Inversion Of Control**: Introduce [Dependency Injection](http://joelabrahamsson.com/inversion-of-control-an-introduction-with-examples-in-net/) by declaring all class dependencies in it’s constructor:

````csharp
public class OrderService
{
    private IOrderSaver orderSaver;
    public OrderService(IOrderSaver orderSaver)
    {
      this.orderSaver = orderSaver;
    }
    public void AcceptOrder(Order order)
    {
      //Domain logic such as validation
      orderSaver.SaveOrder(order);
    }
}
````

- All business code (service, helper, handler, …) must have unit tests
- Keep only the strict necessary visibility for all classes and members.
### **Performances**
- [Premature optimization is the root of all evil](https://www.google.com/search?q=premature+optimization+is+the+root+of+all+evil) ![(blue star)](Aspose.Words.136197ad-a876-40f5-8dfc-d2499b691605.001.png)
  - In consequence, any optimization should be motivate by performance analyses in run condition (profiling, log, …) and result in metrics to measure gain earn when optimization is implemented.
- If a specific optimization code is needed, a comment must be added to explain why and what the optimization code do.
