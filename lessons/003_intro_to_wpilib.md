# Intro to WPILib

WPILib is a framework that handles a lot of things that are required for the robot to start correctly. In order to do this, it enforces some constraints upon our codebase and style, as well as enhancing what we can do within those constraints.

## Command-based programming

This is the main programming style of WPILib. There are other modes in which the library operates, but command-based is the most common by far and the only one we as a team use.

Command-based programming is characterized by two types of classes: subsystems and commands. Subsystems are the simple ones; commands are the bipolar ones (they either take one line or the entire build season).

### Subsystems

Subsystems are classes that extend `SubsystemBase` and represent a part of the robot. A simple example of a subsystem class is AlgaeSubsystem (from our 2025 codebase). Here's the abbreviated file:

```java
// (`package` and imports)

public class Algae extends SubsystemBase {
    private final TalonFX falcon = new TalonFX(Constants.ALGAE_FALCON_ID);

    private TunableNumber grabVolts = new TunableNumber("algae", "grab_volts", AlgaeConstants.GRAB_VOLTS);
    private TunableNumber spitVolts = new TunableNumber("algae", "spit_volts", AlgaeConstants.SPIT_VOLTS);

    public Algae() {
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

Commands, in contrast to subsystems, represent (in a very simple way) actions the robot can take. Note how the above functions are just normal functions. These are fine, but that's not how WPILib works. WPILib uses commands! Note how 'command factories for the above' are cut out from the code snippet. Here's what said command factories look like:

```java
public Command getGrabStop() {
    return startEnd(() -> grab(), () -> stop());
}

public Command getSpitStop() {
    return startEnd(() -> spit(), () -> stop());
}

public Command getStop() {
    return runOnce(() -> stop());
}
```

I told you you needed to understand lambdas. However, to best explain these command factories, it's probably best to use a full Command class. Here's an example:

```java
// (`package` and imports)

public class Grab extends Command {
    private Algae algae;

    public Grab(Algae algae) {
        this.algae = algae;
        addRequirements(algae);
    }

    @Override
    public void initialize() {
        this.algae.grab();
    }

    @Override
    public void execute() {}

    @Override
    public void end(boolean interrupted) {
        this.algae.stop();
    }

    @Override
    public boolean isFinished() {
        return false;
    }
}
```

This command, when *constructed*, stores away the given Algae object for safekeeping (this is an instance of the Algae class from earlier). Then, when *initialized* (something specific to commands), it starts the motor. The `execute` function is run continuously, but doesn't need to do anything, so it's empty (and doesn't need to be there). When the command `end`s, it is told whether it's been interrupted, which is rarely useful but matters sometimes. And the final function, `isFinished`, is called to query whether the command is done with its job and should be done. This command runs until it's told to stop, so it never stops on its own (and because `isFinished` always returns false, `end` is always passed `true`).

Perhaps a bit more information would be beneficial. In WPILib, there's a class called the CommandScheduler. This class schedules and manages all running commands (and their subsystems). If you want, you can look at it by using 'go to definition' on the call to `run()` in Robot#robotPeriodic(). To put it simply:

- When a command is initialized, CommandScheduler calls its `initialize()` function.
- On every tick:
    - Run the `periodic()` (and maybe also `subsystemPeriodic()`) method(s) of all subsystems that have active commands that require them.
    - Call every active command's `execute()` method.
    - Check if any commands are finished (`isfinished()` returns true).
        - If they are, call `end(false)` and remove them from the active commands list.

There are a few other details relevant to using commands, but if you understand this core logic then all commands should be relatively easy to think about.
