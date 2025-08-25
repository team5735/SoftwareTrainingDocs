# WPILib Project Structure and Robot Life Cycle

> This lesson should take about an hour and will walk through the anatomy of a WPILib robot project.

## Introduction

Now that we have our tools set up and understand the basics of Git, it's time to dive into the actual code that makes the robot go. In this lesson, we'll explore the structure of a WPILib project and the life cycle of a robot program.

## Project Structure

When you create a new WPILib project, you'll see a bunch of files and folders. Here's a rundown of the most important ones:

*   **`build.gradle`**: This file is used by Gradle, the build tool we use to compile and deploy our code. You'll rarely need to touch this file.
*   **`.vscode/`**: This folder contains settings for Visual Studio Code, our code editor.
*   **`src/main/java/frc/robot/`**: This is where all of our Java code lives.
    *   **`Constants.java`**: This file holds all of the constants for our robot, such as motor CAN IDs, sensor channels, and PID values.
    *   **`Main.java`**: This is the main entry point for our robot program. You will likely never need to modify this file.
    *   **`Robot.java`**: This is the main class for our robot. It contains the robot's life cycle methods.
    *   **`RobotContainer.java`**: This class is responsible for creating and managing our subsystems, commands, and button bindings.
    *   **`commands/`**: This folder contains all of our command classes.
    *   **`subsystems/`**: This folder contains all of our subsystem classes.

## The Robot Life Cycle

The `Robot.java` file contains several methods that are called at different times during the robot's operation. These methods make up the robot's life cycle.

*   **`robotInit()`**: This method is called when the robot program is first started. This is where you should create your `RobotContainer` and do any other one-time initialization.
*   **`robotPeriodic()`**: This method is called every 20ms, regardless of the robot's mode (disabled, autonomous, or teleoperated).
*   **`disabledInit()`**: This method is called once when the robot enters disabled mode.
*   **`disabledPeriodic()`**: This method is called every 20ms while the robot is in disabled mode.
*   **`autonomousInit()`**: This method is called once when the robot enters autonomous mode.
*   **`autonomousPeriodic()`**: This method is called every 20ms while the robot is in autonomous mode.
*   **`teleopInit()`**: This method is called once when the robot enters teleoperated mode.
*   **`teleopPeriodic()`**: This method is called every 20ms while the robot is in teleoperated mode.
*   **`testInit()`**: This method is called once when the robot enters test mode.
*   **`testPeriodic()`**: This method is called every 20ms while the robot is in test mode.

It's important to understand this life cycle so that you know where to put your code. For example, if you want to run a command at the beginning of the autonomous period, you would schedule it in the `autonomousInit()` method.

## `RobotContainer.java`

The `RobotContainer.java` class is where we bring everything together. In the constructor of this class, we will:

1.  Create instances of our subsystems.
2.  Create instances of our commands.
3.  Create button bindings to link our commands to controller buttons.
4.  Create an autonomous command to run during the autonomous period.

By keeping all of this logic in one place, we can make our code more organized and easier to understand.

## Conclusion

In this lesson, we've learned about the structure of a WPILib project and the life cycle of a robot program. We've also seen how the `RobotContainer.java` class is used to bring everything together. In the next lesson, we'll start writing some code to control motors.