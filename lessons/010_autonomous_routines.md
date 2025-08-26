# Autonomous Routines

> This lesson will cover how to create autonomous routines using commands and command groups.

## Introduction

In the first 15 seconds of an FRC match, the robot operates autonomously, without any driver input. During this time, the robot must be able to score points by itself. In this lesson, we'll learn how to create autonomous routines using commands and command groups.

## Command Groups

A command group is a command that is made up of other commands. Command groups are a powerful tool for creating complex autonomous routines. WPILib provides several types of command groups:

* **`SequentialCommandGroup`**: Runs a list of commands in sequence. The next command in the list will not start until the previous command has finished.
* **`ParallelCommandGroup`**: Runs a list of commands at the same time. The command group will finish when all of the commands in the list have finished.
* **`ParallelRaceGroup`**: Runs a list of commands at the same time. The command group will finish as soon as any of the commands in the list finishes.
* **`ParallelDeadlineGroup`**: Runs a list of commands at the same time. The command group will finish when a specific command (the deadline) finishes.

By combining these command groups, we can create complex and precise autonomous routines.

## Creating an Autonomous Routine

Let's create a simple autonomous routine that drives the robot forward for 3 seconds. First, we need a command to drive the robot forward.

```java
// ... inside the DrivetrainSubsystem class ...

public void drive(double speed) {
    // ... code to drive the robot ...
}

// ... inside a new DriveForward command class ...

public class DriveForward extends Command {
    private final DrivetrainSubsystem drivetrain;
    private final double speed;

    public DriveForward(DrivetrainSubsystem drivetrain, double speed) {
        this.drivetrain = drivetrain;
        this.speed = speed;
        addRequirements(drivetrain);
    }

    @Override
    public void initialize() {
        drivetrain.drive(speed);
    }

    @Override
    public void end(boolean interrupted) {
        drivetrain.drive(0);
    }
}
```

This `DriveForward` command will drive the robot forward at a given speed. It will stop the robot when the command is finished. However, this command will never finish on its own. We need to combine it with a `WaitCommand` in a `SequentialCommandGroup`.

In `RobotContainer.java`, we can create our autonomous command.

```java
// ... inside the RobotContainer class ...

public Command getAutonomousCommand() {
    return new SequentialCommandGroup(
        new DriveForward(drivetrain, 0.5).withTimeout(3),
        // ... other commands ...
    );
}
```

Here, we are using the `withTimeout()` decorator to make the `DriveForward` command finish after 3 seconds. This will cause the `SequentialCommandGroup` to move on to the next command in the list.

## PathWeaver and PathPlanner

For more advanced autonomous routines, we can use tools like PathWeaver and PathPlanner. These tools allow us to create complex paths for the robot to follow. They will generate a trajectory that the robot can follow using PID control and motion profiling.

Using these tools is beyond the scope of this lesson, but it is something that you will likely learn about as you gain more experience.

## Conclusion

In this lesson, we've learned how to create autonomous routines using commands and command groups. We've also seen how to use decorators like `withTimeout()` to control the flow of our autonomous routines. With these tools, you can create autonomous routines that will give your team a competitive advantage.