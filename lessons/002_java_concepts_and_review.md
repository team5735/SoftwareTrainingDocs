# Java Review & New Concepts

> This lesson should go over the basics of Java syntax and organization, **as a review**, then introduce some new concepts, ones that we use frequently for WPILib. Overall, this should take 30-60 minutes

## Intro

We all know something of Java, and today we will guarantee that the core knowledge base is still lingering in your mind. Whether you are actively learning or knew it three years ago, today's lesson should get those gears working again.

In addition, we will learn some new Java features today, some that the College Board (yuck) decided to omit from the APCSA curriculum, though overall they should not be too complicated.

## Java, Line-By-Line

Java has variables, declared, and such. The two main data types are **Primitives** and **Objects**. 

A **Primitive** is one which can be represented by one, unchanging data value. Functionally this means that it is stored differently than its counterpart, though this doesn't matter beyond understanding that Primitives are nicer to your computer and should be used when applicable. The three main Primitive types in Java are:

1. int - a simple number, no decimals, can be positive or negative
2. double - a number, can be positive or negative, but with decimals!
3. boolean - a true/false value (stored by your computer as only one bit, zero or one for true or false)
4. char - a character, such as letters, symbols, or digits (0-9), a group of these are combined to form Strings (we don't really care about char)

An **Object** is a sophisticated data type, and it stores multiple data values (Primitives or more Objects) within it. All Objects belong to a class type, of which you could create infinite! Some examples of classes (Object types) are:

- Arrays - an ordered set of values, all of one type, with a fixed length
- ArrayLists - an ordered set of values, all of one type, but with variable length and other features
- String - an ordered list of characters, effectively a fixed-length Array of characters, but one that can be used for many operations

You may notice that primitive types are written in all lowercase, whereas Objects start with a capitalized letter. Specifically, they are written in CamelCase, meaning that every word has its first letter capitalized and no spaces are employed. Functionally, these capitalization differences are meaningless, but it can be useful to remember such things, as they let you tell the difference in confusing situations.

## Within a Class

Classes tend to follow a basic pattern, allowing for easily reading through to find functionality.

### Instance Variables

An **instance** variable is a value stored within the class, accessible from anywhere within the class, and generally beyond. Specifically, the word **private** before the variable's declaration will make it only accessible to the Class, whereas **public** lets the variable be accessed pretty much anywhere.

Instances are generally placed first in the class's lines.

### Constructors

**Constructors** are methods that return the *same type* as the class they are in and *do not have a unique name*. They can take parameters or not. They tend to come after instance variables but before other methods.

### Methods

**Methods** are Java's effective functions, belonging to a given class. They will have an access level (public or private for most cases), a return type, and any parameters. A return type is simply the data type that the method will return, or `void` meaning that the function will not return any data. Parameters are data values given to the method, and can be referenced from within the method, often determining the returned value.

## Inheritance

**Inheritance** is the big spooky word of APCSA, but it shouldn't be too much to worry about. Simply put, inheritance lets you create different classes based off of a pre-existing class, giving them all the same methods of the "parent". Because these "sub-classes" have all the data of their parents, they can be treated as belonging to the parent class, letting us use them in place of the parent. 

On a line-by-line basis, parent methods can be overwritten to give new functionality in a subclass, provided that they have the same name, return type, and parameter type/order.

## New Things

Ok, review over, time to really learn some new stuff (unless you already learned some of this, or they updated the APCSA curriculum).

### Static and Final

These two are simple, they are modifiers placed before a variable, similar to public/private. `static` will make it so that the variable will not change across different instances of the class, meaning that it is tied to the class file itself, not the objects belonging to the class. `final` simply means that a data value will never change, and should be relatively straightforward.

When accessing a `public static` variable, the syntax is `FileName.variableName`, though we tend to write it as `FileName.VARIABLE_NAME` because its cooler and lets us differentiate how values are used (this will be elaborated on next lesson).

### Enums

An enum is basically a class, but with pre-saved instances of that class. They are useful when tracking limited options that are greater than two, where a boolean simply would not work, and where using an int for identification could lead to errors. Syntactically, basic enums are declared as such:

	public enum Thing{
		VERSION1,
		VERSION2,
		VERSION3;
	}
 
where each version is in all caps, separated by commas, and ended by a semicolon. Enums can also have instance fields, and constructors. When an enum has a constructor with parameters, its versions must be followed by parameters for said constructor:

	public enum BetterThing{
		VERSION1(35),
		VERSION2(42),
		VERSION3(9000);
	
		public int coolNum;
		
		Betterthing(int coolNum){
			this.coolNum = coolNum;
		}
	}

Each version is effectively its own call to the constructor, storing a unique instance while saving its name also. Note that the enum constructor does not generally have public or private in front of it, and that enum type names are capitalized and in CamelCase.

### Lambda Functions

Ok, this name sounds scary and cool, but really these are only the latter. **Lambda Functions** are functions (similar to methods) that can be used like Objects (because they are). They are sometimes called "Anonymous Functions" because they don't have a name.

The best way to explain a Lambda Function is by example, so here is an excerpt from the 2024 robot code (also on the Sample Codebase, in AngleSubsystem.java)

	FactoryCommands.runOnceUntil(
		    ()  -> setSetpoint(angle),  ()  -> isAtPosition(angle)
		);
	
In this case, `FactoryCommands.runOnceUntil()` is defined as taking a `Runnable` and a `Supplier<Boolean>`.  A Runnable is a type of Lambda Function, which takes no parameters and one expression, a block of code that can be run. Our syntax reflects that, where `() ->` represents any parameters in the parenthesis, as we would with a real method, and the arrow leading to the actual expression, here `setSetpoint(angle)`, a generic void method taking in some parameter `angle`. A `Supplier` is similarly parameterless, but instead of an action to be executed, its code block must have a return, whatever data type is placed between the `<>` in its type declaration. In our case this is a boolean, meaning that we must give it code that returns a boolean, here the method `isAtPosition(angle)`, which is a method that will return true/false, or a boolean returning method.

If we instead wanted to create new code exclusively for this situation, we could have written `() -> { new code }` where the curly brackets represent the function of the lambda.

This may all be a little confusing as, but as you work with lambdas in code, you should hopefully build a sufficiently advanced understanding of them, for there is not much more to them than what has been here outlined. 
