# Subsystems

> (as of now) simply an overview of the point of subsystems and what they represent

## The structure

WPILib, as a library, contains some classes to help you structure your code. Subsystems and Commands are the most important of these, and today we will be covering subsystems.

### Representation

Subsystems are a simple idea with rather complex execution, but once you learn and understand how they work it all makes sense (for the most part).
In short, subsystems represent a part of the robot (hence the prefix sub-). For example, in last year's robot, we had a subsystem to represent each of the climbers, one to represent the angle changer, one for the shooter, one for the drivetrain, and so on and so forth, breaking up our robot's code in much the same way as our team is.
We create a subsystem by subclassing the `SubsystemBase` class; this enables WPILib to manage our all subsystems we might create in exactly the same way. You don't need to write your own class from scratch every single time, however; WPILib for VSCode has a fancy feature which will generate a subsystem for you if you ask nicely.
The subsystem that WPILib generates includes a few skeleton functions which outline the programmatical structure of a subsystem quite well, so let's go over them!

### A subsystem's default functions

#### The constructor

As you hopefully remember from APCSA, a constructor's job is to ensure that an object is ready for use. Applying this concept to the idea of a subsystem, we understand that the constructor is there to set up any relations with the rest of the robot or code that the given subsystem might have.
For example, the constructor might initialize communication with a motor, enabling the rest of the subsystem to use said motor, and perhaps also setting defaults for the motor's parameters.

#### Method commands

These are called 'command factories' here in Control Freaks. They're simple to understand after you learn what commands are and what they do, but until that lesson comes, I'll just leave you with this: they're simple methods that return `Command` objects, and they're used so that we don't have to make an entire class for a simple one-function command; we can instead just make use of command factories and write what would take 20 lines of boilerplate and a new file in about three lines.

#### Condition functions

These are actually really simple as they aren't special to WPILib: they aren't called for seemingly no reason (foreshadowing?), they don't return WPILib-specific classes...
These are just simple methods that are almost always used to query internal components of a subsystem. They're essentially 'getters,' if you remember what those are!

#### Do-something functions

This name is noticeably less official, but that doesn't mean it's less important.
In the name of preserving encapsulation, subsystems traditionally keep their internal data and handles private, such as motor-controlling classes or PID controllers (which you'll learn about later) and expose a public interface to tell them what to do with what and when. This interface is composed of nothing more than these do-something functions and the conditions functions.
Commands are the structure that tie together these two types of functions, by containing code that queries state and then makes decisison based off of that state, telling these do-something functions to perform the desired action, such as spinning a motor or moving the robot.

#### Periodic

Periodic is a special function. Remember how I mentioned earlier that the purpose of having every subsystem subclass SubsystemBase was so that WPILib could manage the subsystem for us?
Well, this is a perfect example of that. But to understand exactly what 'periodic' does, it's best you understand the scheduler, but before explaining that, I'll quickly introduce one last function: simulationPeriodic.

#### SimulationPeriodic

This function is just like periodic, except it's called during the simulation. It can be used to do simulation-specific hackery (which is a bad idea as the point of a simulation is to be as close to reality as possible), and that's about it.

## The scheduler

The scheduler is a so-called singleton class, which means that only one copy of it exists, ever. (The One Copy can be retrieved using CommandScheduler.getInstance().)
The command scheduler has one important method that does all its magic: `run`. `run` is responsible for running periodic methods of registered subsystems, polling buttons, running commands (later!), managing commands, and more.
But what we're interested in is the part that has to do with subsystems. Commands can 'require' a subsystem, which is a declaration that that command will use that subsystem, and when a command scheduled to the CommandScheduler requires a subsystem, the scheduler remembers that subsystem and then calls its .periodic method every time its `run` method is called.
Now, let's ask 'why' again - what is `run`'s purpose at all and when is it called?
The first question has a rather simple answer; it's the beating heart of a command-based robot (what we're doing), and calling it is required before the rest of the WPILib framework will work.
It's called every so-called tick and actually does the vast majority of a tick's work. It polls buttons (checks for button and controller updates, in other words), runs commands and runs peoriodic on subsystems.

### Interaction with RobotContainer

The RobotContainer owns all the subsystem instances. It constructs them in its constructor but doesn't typically get involved in the logic; it lets the Commands it sets up do that instead.

## Summary

The subsystems in the WPILib command-based framework, the one we use, each represent a part of the robot, and they each manage the part they represent.
Subsystems expose methods to query and control the part they represent, enabling commands to work with their corresponding subsystem(s), making the whole robot move.
