# C# Coding Standards

These coding standards should act as a guideline for writing consistent, legible, robust, manageable and modern C#.

## Purpose

## Table of Contents

1. [`.cs` File Layout](#cs-file-layout)
1. [Directory Layout](#directory-layout)
1. [Declarations](#declarations)
1. [Casing](#casing)
1. [Indentation](#indentation)
1. [Spacing](#spacing)
1. [Statements](#statements)
1. [Naming Conventions](#naming-conventions)
1. [Documenting Code](#documenting-code)
1. [Initializing Objects and Collections](#initializing-objects-and-collections)
1. [Long Argument Lists](#long-argument-lists)
1. [Error Handling](#error-handling)
1. [Programming Practices](#programming-practices)


## `.cs` File Layout
[Jump to Table of Contents](#table-of-contents)

Keep your classes/files short, don't exceed 2000 LOC (lines of code), divide your code up, make structures clearer. Put
every class in a separate file and name the file like the class name (with .cs as extension of course). This
convention makes things much easier.

Lay out your C# code in a `.cs` file that looks like this:

```
Using Directives

Namespace Declaration

	Type Declaration
		Constants
		
		Static Fields
		
		Static Auto-Properties
		
		Static Constructor
		
		Static Methods
		
		Fields
		
		Auto-Properties
		
		Constructors
		
		Complex Properties
		
		Methods
```

Here is an example Database Context file that follows this convention.

`DataContext.cs`
```csharp
// Using Directives
using System;
using System.Data;
using System.Data.Entity;

using MyLib;
using MyLib.Core;

// Namespace Declaration
namespace MyLib.Data
{
	// Type Declaration
	public class DataContext : DbContext
	{
		// Constants
		public const string DatabaseName = "MyLibDb"
		
		// Static Fields
		public static bool Stage = true;
		
		// Static Auto-Properties
		public static bool Fast { get; set; }
		
		// Static Constructor
		public static DataContext()
		{
			Fast = true;
		}
		
		// Static Methods
		public static DataContext CreateNew()
		{
			return new DataContext();
		}
		
		// Fields
		private readonly ISession _session;
		
		// Auto Properties
		public IDbSet<Order> Orders { get; set; }
		public IDbSet<Customer> Customers { get; set; }
		public IDbSet<Account> Accounts { get; set; }
		
		// Constructors
		public DataContext() : base(DatabaseName)
		{
			
		}
	
		// Complex Properties
		public ISession Session
		{
			get { return _session; }
			set { _session = value; }
		}
		
		// Methods
		protected override void OnModelCreating(DbModelBuilder dbModelBuilder)
		{
			
		}
	}
}
```

## Directory Layout
[Jump to Table of Contents](#table-of-contents)

### Reflect your namespaces in your directory structure

For example, if you want a root namespace called `OriginCodeAcademy` with three child namespaces - `OriginCodeAcademy.Core`, `OriginCodeAcademy.Data` and `OriginCodeAcademy.API`, then you would create an `OriginCodeAcademy` solution with three projects, demonstrated below.

`Legend`
```
+   Solution
-   Project
/   Directory
.   File
```
```
+ OriginCodeAcademy
	- OriginCodeAcademy.Core
		/ Domain
			. Student.cs
			. Course.cs
		/ Repository
			. IStudentRepository.cs
			. ICourseRepository.cs
	- OriginCodeAcademy.Data
		/ Infrastructure
			. OriginDbContext.cs
		/ Repository
			. StudentRepository.cs
			. CourseRepository.cs
	- OriginCodeAcademy.API
		/ Controllers
			. StudentsController.cs
			. CoursesController.cs
```

### Create a directory for 3rd level and deeper namespaces.
Note that in [Reflect your namespaces in your directory structure](#reflect-your-namespaces-in-your-directory-structure), any namespace three levels or deeper is specified as folders within the containing project/folder. Our template for namespaces then is as follows.

`[Solution].[Project].[Folder].[Folder].[Folder]`

Try to keep your namespaces 5 or less levels deep.

Example
```
+ MyLib
 	- MyLib.Core
	 	/ Domain
	 		/ Order
				. Order.cs
			/ Account
				. Account.cs
			/ Customer
				. Customer.cs
				. CustomerPhone.cs
				. CustomerEmail.cs
```

## Declarations
[Jump to Table of Contents](#table-of-contents)

### Declaring Types
Leave an empty line between every type definition:

```csharp
// Good.
namespace MyLib.Core
{
	public enum Direction { Left, Right }

	public class ImportantThing
	{
		//
	}
}

// Bad - missing and empty line between type definitions.
namespace MyApp
{
    public enum Direction { Left, Right }
    public class ImportantThing
    {
        //
    }
}

// Bad - more than one empty line.
namespace MyApp
{
    public enum Direction { Left, Right }


    public class ImportantThing
    {
        //
    }
}
```

### Declaring Enums
enums in C# should be given pluralized names so as to distinguish them from names of classes, that describe a single responsibility/concept/object.

Examples: 
```csharp
// Good.
public enum Directions { North, South, East, West }

// Bad.
public enum PhoneType { Home, Work, Mobile }
```

Simple enums can be defined in a single line, however more complex enums (specifically ones where you assign a value to each enum member) should be defined on multiple lines.

```csharp
// Good - this is a simple enum defined on one line.
public enum Edges { Left, Right, Bottom, Top }

// Good - this is a complex enum defined on multiple lines.
public enum PhoneTypes
{
	Home = 1,
	Work = 2,
	Mobile = 3
}
```

## Casing
[Jump to Table of Contents](#table-of-contents)

Microsoft wants you to use `PascalCase` or `camelCase` only in C#. The following table summaries the casing rules for identifiers and provides examples for the different types of identifiers.

<table>
	<thead>
		<tr>
			<th>Identifier</th>
			<th>Case</th>
			<th><strong>Example</strong></th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Namespace</td>
			<td>PascalCase</td>
			<td><strong>OriginCodeAcademy.Core.Domain</strong></td>
		</tr>
		<tr>
			<td>Enumeration type</td>
			<td>PascalCase</td>
			<td><strong>PhoneTypes</strong></td>
		</tr>
		<tr>
			<td>Enumeration values</td>
			<td>PascalCase</td>
			<td><strong>Work</strong></td>
		</tr>
		<tr>
			<td>Class</td>
			<td>PascalCase</td>
			<td><strong>DataContext</strong></td>
		</tr>
		<tr>
			<td>Interface</td>
			<td>PascalCase</td>
			<td><strong>IEnumerable</strong></td>
		</tr>
		<tr>
			<td>Constants</td>
			<td>PascalCase</td>
			<td><strong>DbName</strong></td>
		</tr>
		<tr>
			<td>Public Members</td>
			<td>PascalCase</td>
			<td><strong>Students</strong></td>
		</tr>
		<tr>
			<td>Method</td>
			<td>PascalCase</td>
			<td><strong>OnModelCreating</strong></td>
		</tr>
		<tr>
			<td>Private Members</td>
			<td>camelCase</td>
			<td><strong>doSomethingInternal</strong></td>
		</tr>
		<tr>
			<td>Method Parameter</td>
			<td>camelCase</td>
			<td><strong>typeName</strong></td>
		</tr>
		<tr>
			<td>Local Method Variables</td>
			<td>camelCase</td>
			<td><strong>tempStore</strong></td>
		</tr>
	</tbody>
</table>

## Indentation
[Jump to Table of Contents](#table-of-contents)

When an expression will not fit on a single line, break it up according to these general principles:

- Break after a comma `,`.
- Break after an operator `+ - / * && || > < >= <= == !=`
- Align the new line with the beginning of the expression at the same level on the previous line

Example: Breaking up a large Lambda Expression
```csharp
var studentsMatchingTerm = db.Students.Where(s => s.FirstName.Contains(searchTerm) ||
												  s.LastName.Contains(searchTerm) ||
												  s.EmailAddress.Contains(searchTerm));
``` 

Example: Breaking up a chain of method calls
```csharp
// Good - Method calls are broken into multiple lines and aligned with eachother
modelBuilder.Entity<Student>()
			.HasMany(s => s.Projects)
			.WithRequired(p => p.Student)
			.HasForeignKey(p => p.StudentId);
			
// Bad - Some method calls are not broken into multiple lines and are not aligned with eachother
modelBuilder.Entity<Student>().HasMany(s => s.Projects)
	.WithRequired(p => p.Student).HasForeignKey(p => p.StudentId);
```

Example: Breaking up a large arithmetic expression
```csharp
// Good - Breaks after an operator
var result = a * b / (c - g + f) +
			 4 * z;
			 
// Bad - Breaks before a bracket expression closes
var result = a * b / (c - g +
			 f) + 4 * z;
```

## Spacing
[Jump to Table of Contents](#table-of-contents)

### Tabs vs Spaces
An indentation standard for C# was never achieved, and is down to personal preference. What is most important is that you are consistent with your indentation.

At Origin - we advise you to stick with the Visual Studio convention - use tabs to indent - and use the default indent size of 4 spaces. You don't have to change anything in Visual Studio - this is the default.

Example (Using hyphens to indicate spaces)
```csharp
using System;

namespace MyApp
{
----public class Program
----{
--------public static void Main(string[] args)
--------{
------------Console.WriteLine("Hello World");
--------}
----}
}
```

### Blank Lines
Blank lines improve readability. They provide visual clarity between blocks of code that are logically related.

#### Use one blank line for
- Methods
- Properties
- Local variables in a method and its first statement
- Logical sections inside a method to improve readability

#### Use two blank lines for
- Logical sections of a source file
- Class and interface definitions (Put classes/interfaces in their own file to prevent this case)

## Statements
[Jump to Table of Contents](#table-of-contents)

### Each line should contain only one statement
```csharp

// Good
int x = 5; 
int y = 10;

// Good
int x = 5,
	y = 10;
	
// Bad
int x = 0; y = 10;

// Bad
int x = 0, y = 10;
```

### A return statement should not use outer most parentheses.
```csharp
// Good
return n * (n + 1) / 2;

// Bad
return (n * (n + 1) / 2);
```

### `if` statements
```csharp
// Good
if(price > 50)
{
	// Reduce price by 5%
	return price - (price * 0.05);  
}
else
{
	return price;
}

// Bad
if (price > 50) {
	return price - (price * 0.05);
} else {
	return price;
}
```

### `for` / `foreach` statements
```csharp
// Good
for(int i = 0; i < 10; i++)
{
	Console.WriteLine(i);
}

// Acceptable - Braces not needed in a loop containing only one statement
for(int i = 0; i < 10; i++)
	Console.WriteLine(i);

// Bad
for(int i = 0; i < 10; i++) {
	Console.WriteLine(i);
}

// Good
foreach(var student in db.Students)
{
	student.AssessGrades();
}

// Acceptable - Braces not needed in a loop containing only one statement
foreach(var student in db.Students)
	student.AssessGrades();

// Bad
foreach(var student in db.Students) {
	student.AssessGrades();
}
``` 

### `while` statements
```csharp
// Good
while(cohort.WeeksLeft > 12)
{
	cohort.TeachWeek();
}

// Acceptable - Braces not needed in a loop containing only one statement
while(cohort.WeeksLeft > 12)
	cohort.TeachWeek();
	
// Bad
while(cohort.WeeksLeft > 12) {
	cohort.TeachWeek();
}
```

### `switch` statements
```csharp
// Good
switch(condition) 
{
	case A:
		//
		break;
	case B:
		//
		break;
	default:
		//
		break;	
}

// Bad (awful)
switch(condition) {
case A:
	break;
	case B:
	break;
case C:
		break;
}

```

### `try-catch` statements
```csharp
// Good
try
{
	// do something
}
catch (Exception e)
{
	// handle exception
}

// Bad
try {
	// do something
}
catch (Exception e) {
	// handle exception
}
```

## Naming Convention
[Jump to Table of Contents](#table-of-contents)

### Label variables as clearly as possible
```csharp
// Good
var fullName = "John Smith";

// Bad
var x = "John Smith";
```

### Do not shorten variable names
```csharp
// Good
var sumOfAccountingEntries = db.AccountingEntries.Sum(ae => ae.Balance);

// Bad
var sumAccntEtrs = db.AccEnt.Sum(ae => ae.Bal);
```

### Use single character variable names sparingly
```csharp
// Good use of single character variable
for(int i = 0; i < 10; i++)
	Console.WriteLine(i);
	
// Good use of single character variable
try
{
	// do something
}
catch (Exception e)
{
	// handle exception
}

// Bad use of single character variable
decimal x = db.AccountingEntries.Sum(ae => ae.Balance);

// Better use in this scenario
decimal sumOfAccountingEntries = db.AccountingEntries.Sum(ae => ae.Balance);
```

### Do not infer type in variable names 
E.g. `string sName = "Cameron";`. This is redundant in a strongly typed language such as C#. The exception to this rule is when you are converting a variable from one type to another in a local method.
```csharp
Console.WriteLine("Enter your birth date");
string strBirthDate = Console.ReadLine();
DateTime birthDate = DateTime.Parse(strBirthDate);
```

## Documenting Code
[Jump to Table of Contents](#table-of-contents)

## Initializing Objects and Collections
[Jump to Table of Contents](#table-of-contents)

## Long Argument Lists
[Jump to Table of Contents](#table-of-contents)

## Error Handling
[Jump to Table of Contents](#table-of-contents)

## Programming Practices
[Jump to Table of Contents](#table-of-contents)