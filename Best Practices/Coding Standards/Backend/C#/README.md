# C# Coding Standards

These coding standards should act as a guideline for writing consistent, legible, robust, manageable and modern C#.

## Purpose

## Table of Contents

1. [`.cs` File Layout](#.cs-file-layout)
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

## Spacing
[Jump to Table of Contents](#table-of-contents)

## Statements
[Jump to Table of Contents](#table-of-contents)

## Naming Convention
[Jump to Table of Contents](#table-of-contents)

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