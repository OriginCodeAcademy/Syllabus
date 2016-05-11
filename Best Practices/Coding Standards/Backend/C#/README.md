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

This section aims to show you how to organize code in your C# files in a standard and consistent way.

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

## Declarations

## Casing

## Indentation

## Spacing

## Statements

## Naming Convention

## Documenting Code

## Initializing Objects and Collections

## Long Argument Lists

## Error Handling

## Programming Practices