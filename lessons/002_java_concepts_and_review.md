# Java concepts and review

## Intro

Welcome to our second lesson!

If you've taken APCSA or otherwise know Java, this will be a review — feel free to tune us out until we get to the cooler stuff.  If you're otherwise familiar with programming, you should be able to follow as we introduce Java's versions of basic concepts. If you don't know any programming, you can still follow if you put in the effort to learn how to think for coding as you go, whether that be by asking other software members or the leadership or the internet.

And if you'd like to play with some code as you go, you can mess around in the example repository that you cloned last time. You can always throw away anything you don't like.

Even if you took APCSA, we'll cover some cool Java features that you might not have seen before, so pay attention for those. These work nicely with WPILib to help us write better code.

## Introduction to Java

### Java data types

**Primitives:** These are relatively simple and small in number.

* `int`: A whole number (e.g., 1, -5, 100).
* `double`: A number with a decimal point (e.g., 3.14, -0.5).
* `boolean`: Either true or false.
* `char`: A single character encased in single quotes (e.g., 'a', '!', '7').

**Objects:** These are more complex data types with their own capabilities.

* `String`: A sequence of characters encased in double quotes (e.g., "Hello, world!").
* `Array`: A fixed-size list of items of the same type (e.g., {1, 2, 3}, {"Rayan", "am", "goated!"}).
* `ArrayList`: A resizable list of items of the same type (which look the same).
* ... and many, many more ...

> [!TIP]
> Notice how primitive types are all lowercase, while object types start with a capital letter. That's a handy way to tell them apart!

### Classes

In Java, all of our code lives inside of **classes**. A class, most succinctly, represents a blueprint for something, and can be compared to the blueprint of a house. Instances of classes can be created, often referred to as objects, and can be compared to the fully constructed house that originates from the blueprint. Here's the typical structure of a class:

* **Instance Variables:** These are variables that belong to the class itself. They're usually declared at the top of the class and define the properies of the thing.
* **Constructors:** A constructor is a special method that gets called when you create a new object from the class. It's like the object's setup wizard.
* **Methods:** Methods are the actions that an object can perform. They tell you what this thing can do.

Defining a new class defines a new type of object. The classes listed above under 'objects', therefore, have this same format.

### Inheritance

**Inheritance** is a fancy word for a simple idea: you can create a new class that's based on an existing class. The new class (the "subclass") inherits all the methods and variables of the original class (the "parent class"), and can be referenced without any prior mention inside the subclass.

This is super useful because it lets us reuse code and create specialized versions of our classes. We don't use this much in robot code (preferring interfaces, thanks to WPILib's design) but you should still know that inheritance is spelled like this in Java:

```java
class Subclass extends Superclass {
    // ...
}
```

## Fanciness inbound!

If you were tuning us out, now's the time to listen up. These aren't covered in your average APCSA course, but are more common in other languages.

> [!WARNING]
> If you do not understand everything mentioned above, then please let us know and we will try to review it.
> It will be even more difficult to understand what lies ahead without a foundational understanding fo the basics.

### `static` and `final`

These are special keywords that you can add to a variable.

* `static`: A `static` variable is shared by all instances of a class. It's like a global variable for that class.
* `final`: A `final` variable can only be assigned a value once. It's a constant. You cannot change this variable elsewhere while your program is running.

> [!IMPORTANT]
> We usually write `final` variable names in all caps, with underscores to separate words (e.g., `MAX_SPEED`).
> You can find other conventions like this in style-guide.md in the main folder of this repository.

### Enums: The Picky Eater's Best Friend

An **enum** is a special type of class that lets you define a set of constant values. It's perfect for when you have a limited number of modes or options for something.

For example, you could use an enum to represent the different states of a shooter: `IDLE`, `SPINNING_UP`, `READY_TO_SHOOT`. A traffic light could also be represented by an enum, with its states of `RED`, `YELLOW`, and `GREEN`.

### Lambda Functions: The Cool Kid on the Block

**Lambda functions** (or "lambdas" for short) are like mini-methods that you can create on the fly. They're a concise way to write code that you only need to use once, rather than create a whole new funtion in the space of one's code.. If a function is a reusable straw, thena a lambda is a single-use straw.

The main conceptual leap with lambdas is that you can treat them as objects. Here's some example code that *might* help, but it's no problem if it doesn't:

```java
// (inside a class)
void runYourLambda(Runnable fun) {
    System.out.println("running!");
    fun.run();
    System.out.println("done!");
}

void lambdasAreObjects() {
    runYourLambda(() -> System.out.println("Lamdba 1!"));
    System.out.println("Ok, running the second lambda now");

    int myNumber = 10;
    runYourLambda(() -> {
            System.out.println("This lambda runs basically any code it would like.");

            System.out.println("The number I'm holding is " + myNumber);
            System.out.println("Let me square that: " + myNumber * myNumber);
    });
}
```

Don't worry if this sounds confusing at first. You'll get the hang of it as you see it in action. Remember that you can always come back to this code and try to understand it more. If you need somebody else to explain it, the internet or your favorite AI will be happy to oblige.

### Interfaces: The Rule-Makers

An **interface** is like a contract for a class. It defines a set of methods that a class must have, but it doesn't say how those methods should work. It's up to the class to provide the implementation.

Interfaces are a great way to make sure that different classes have a consistent set of abilities.

A good example of an interface is the Subsystem interface from WPILib. If a class `implements Subsystem`, then we know we can treat it as a Subsystem because it's said that that's what it is.

At pain of dying by repetition, I'll say again that you can find these lesson documents at `https://github.com/team5735/SoftwareTrainingDocs`.

## Units

Units are a relatively new feature in WPILib, but they're very welcome. They let us write safer code — that means code that's harder to make mistakes with — by using the type system in Java to automagically convert between units as needed.

There are a few types of unit classes. Assuming you're set up correctly, you should be able to use them without issue, as long as you autocomplete the unit names.

Each unit has two (sometimes more) classes associated with it. To help explain units, take the example of meters per second. `MetersPerSecond` defines what a meter per second is, and you use it to construct the associated type of `LinearVelocity`. (Technically, `MetersPerSecond` is a constant of type `LinearVelocityUnit`.)

How do we use them? It's simple:

```java
// robotSpeed represents 1.0 m/s
LinearVelocity robotSpeed = MetersPerSecond.of(1.0);

// shotSpeed represents 2.0 ft/s
LinearVelocity shotSpeed = FeetPerSecond.of(2.0);

// WPILib automatically converts units for us. The resulting value doesn't really
// have a defined unit ...
LinearVelocity projectileSpeed = shotSpeed.plus(shotSpeed);
// ... but we can ask for it as a `double` in a specific unit:
double projectileSpeedMPS = projectileSpeed.in(MetersPerSecond);
```

You can pass these around as normal values, and the expected operations work on them:

- `a.plus(b)` is the same as `a + b`
- `a.minus(b)` is the same as `a - b`
- `a.times(b)` is the same as `a * b`
- `a.div(b)` is the same as `a / b`
- `a.unaryMinus()` is the same as `-a`

And there's one last thing you should know: to compare two `Measure`s (`LinearVelocity` is officially a `Measure`) you have to do this:

```java
// (using our speeds from earlier)
if (robotSpeed.compareTo(shotSpeed) > 0) {
    System.out.println("The robot is faster than the shot.");
} else if (robotSpeed.compareTo(shotSpeed) < 0) {
    System.out.println("The robot is slower than the shot.");
} else if (robotSpeed.equals(shotSpeed)) {
    System.out.println("The robot is the same speed as the shot.");
} else {
    System.out.println("This shouldn't happen.");
}
```
