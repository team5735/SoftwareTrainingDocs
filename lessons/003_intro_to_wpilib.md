# Intro to WPILib

WPILib is a framework that handles a lot of things that are required for the robot to start correctly. In order to do this, it enforces some constraints upon our codebase and style, as well as enhancing what we can do within those constraints.

## Command-based programming

This is the main programming style of WPILib. There are other modes in which the library operates, but command-based is the most common by far and the only one we as a team use.

Command-based programming is characterized by two types of classes: subsystems and commands. Subsystems are the simple ones; commands are the bipolar ones (they either take one line or the entire build season).

### Subsystems

Subsystems are classes that extend `SubsystemBase` and represent a part of the robot. A simple example of a subsystem class is AlgaeSubsystem (from our 2025 codebase). Here's the abbreviated file:

```java
// (`package` and imports)

public class AlgaeSubsystem extends SubsystemBase {
    private final TalonFX falcon = new TalonFX(Constants.ALGAE_FALCON_ID);

    private TunableNumber grabVolts = new TunableNumber("algae", "grab_volts", AlgaeConstants.GRAB_VOLTS);
    private TunableNumber spitVolts = new TunableNumber("algae", "spit_volts", AlgaeConstants.SPIT_VOLTS);

    public AlgaeSubsystem() {
        falcon.getConfigurator().apply(new MotorOutputConfigs().withNeutralMode(NeutralModeValue.Brake));
    }

    public void grab() {
        falcon.setVoltage(grabVolts.get());
    }

    public void spit() {
        falcon.setVoltage(-spitVolts.get());
    }

    public void stop() {
        falcon.setVoltage(0);
    }

    // (command factories for the above)
}
```

As you can see, the core of this class is really not all that complicated, reflecting the simplicity of its physical counterpart. The algae subsystem doesn't really do anything other than move a single motor back and forth, and so the subsystem just has an instance variable for the motor as well as some functions to do stuff with that motor. The real action comes when you look at commands.

### Commands

Commands, in contrast to subsystems, represent (in a very simple way) actions the robot can take. Note how the above functions are just normal functions. These are fine, but that's not how WPILib works. WPILib uses commands! Note how 'command factories for the above' are cut out from the code snippet. Don't worry about those. To best explain these commands, it's best to use a full Command class. Here's such a class:

```java
// (`package` and imports)

public class GrabCommand extends Command {
    private AlgaeSubsystem algae;

    public GrabCommand(AlgaeSubsystem algae) {
        this.algae = algae;
        addRequirements(algae);
    }

    @Override
    public void initialize() {}

    @Override
    public void execute() {
        algae.grab();
    }

    @Override
    public void end(boolean interrupted) {
        algae.stop();
    }

    @Override
    public boolean isFinished() {
        return false;
    }
}
```

This command, when *constructed*, stores away the given Algae object for safekeeping (this is an instance of the Algae class from earlier). Then, when *initialized* (something specific to commands and different from construction), it starts the motor. The `execute` function is run continuously, but doesn't need to do anything, so it's empty (and doesn't need to be there). When the command `end`s, it is told whether it's been interrupted, which is rarely useful but matters sometimes. And the final function, `isFinished`, is called to query whether the command is done with its job and should be done. This command runs until it's told to stop, so it never stops on its own (and because `isFinished` always returns false, `end` is always passed `true`).

Believe it or not, an instance of Grab does almost exactly the same thing as `getGrabStop()` from the command factories. The function `runEnd()` (available inside subsystems, elsewhere you should use `Commands.runEnd(lambda, lambda, requirements...)`, which is identical given the correct requirements) is one of many command factory-enabling functions, along with `run()` (runs the lambda forever with no ending function), `runOnce()` (runs the lambda once and finishes immediately), and many others you can find [here](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/wpilibj2/command/Commands.html) are all incredibly useful for writing less code that does more, which we want.

Perhaps a bit more information would be beneficial. In WPILib, there's a class called the CommandScheduler. This class schedules and manages all running commands (and their subsystems). If you want, you can look at it by using 'go to definition' on the call to `run()` in Robot#robotPeriodic(). To put it simply:

- When a command is initialized, CommandScheduler calls its `initialize()` function.
- On every tick:
    - Run the `periodic()` (and maybe also `subsystemPeriodic()`) method(s) of all subsystems that have active commands that require them.
    - Call every active command's `execute()` method.
    - Check if any commands are finished (`isfinished()` returns true).
        - If they are, call `end(false)` and remove them from the active commands list.

There are a few other details relevant to using commands, but if you understand this core logic then all commands should be relatively easy to think about.

## Actually using commands in practice

Only in rare advanced scenarios are commands manually scheduled. Typically, WPILib schedules them for us, primarily through the use of triggers. Triggers are a complex subject that we'll cover in full later (if at all formally), but for now all you need to know is that a `Trigger` object represents a boolean value through time (at each tick). By far the most common trigger is from command-based controllers:

```java
// (in RobotContainer, typically)
private final CommandXboxController driveController = new CommandXboxController(Constants.DRIVE_CONTROLLER_PORT);

private final AlgaeSubsystem algae = new AlgaeSubsystem();

// in configureBindings
driveController.a().whileTrue(new GrabCommand(algae));
```

There's a few things I'd like to point out about this example. First of all, `driveController` and `algae` are instances of the `RobotContainer`. Second, `driveController.a()` is a trigger representing the A button on the Xbox controller at that port (typically 0 in our projects, this refers to the port in the FRC Driver Station). This means that when A is pressed, driveController.a() is true.

The method `Trigger#whileTrue(Command)` 'registers' (loosely speaking) the passed Command object to be scheduled (with `Command#schedule()`) when the trigger goes from false to true and cancelled (interrupted) when the trigger goes from true to false. In this case, that would make the motor associated with this algaer start spinning when the button is pressed and stop when it's released.

---

# Task

Here are the three tasks:

1. Make a `MotorCommand` and `MotorSubsystem` modelling the above command and subsystem examples (you can also look at `ExampleCommand` and `ExampleSubsystem`). Bind an instance of that `MotorCommand` to the a button with the line `m_driverController.b().whileTrue(new MotorCommand(motor));` and make it so that the motor's voltage is set to 1 when the button is pressed and set to 0 when the button is released (with `setVoltage`).

2. Now, modify your `MotorSubsystem` and `MotorCommand` to handle two motors at once. Only one should run at each time, and instead of running one motor, the a button should *switch* which motor is running.

3. Modify those same classes to have the motor speed reflect the right trigger. Specifically, the voltage of whichever motor is running should be set to 1 + the trigger.
