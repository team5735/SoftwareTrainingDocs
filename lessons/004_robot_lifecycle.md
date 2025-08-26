# Robot Lifecycle

## A Place for Everything

When you open up our robot code, there are a lot of files and folders, but 90% of your time will be spent within `src/main/java/frc/robot`.

* **`Robot.java`**: This runs the command-based framework.
* **`RobotContainer.java`**: This is where we set up all our subsystems and commands and bind buttons.
* **`subsystems/`**: Subsystem classes. Generally one exists for each discrete part of the robot.
* **`commands/`**: Command classes. In production code, this is mostly larger commands and more complex tasks.
* **`constants/`**: Constants files. Generally one exists for each subsystem.

## The Circle of Life

The `Robot.java` file has a bunch of methods that get called at different times. This is the robot's **lifecycle**.

Generally, you don't need to worry about this too much - all they do is setup and manage the command-based system - but it's good to know what's happening.

* **`robotInit()`**: Called when you first turn on the robot.
* **`robotPeriodic()`**: Called every tick (20ms) while the robot is running (runs the execute method of commands).

Equivalent methods exist for disabled, autonomous, and teleop, but these two are always run.

## The `RobotContainer`: Your Robot's Mission Control

RobotContainer, when constructed, sets up controller buttons to map to certain commmands, creates subsystems, and more.

By keeping all of this logic in one place, you'll make your code more organized and easier to understand.

It's declarative, which is a style of coding that basically means you write code like 'when button A is pressed, run command X' instead of checking for A being pressed every tick.

## What's Next?

Now that you know the lay of the land, it's time to start building! In the next lesson, we'll get our hands dirty and learn how to control motors.
