# Basic motor control

## The Brains Behind the Brawn

To control a motor, we need a **motor controller**. This is a small electronic device that sits between the RoboRIO and the motor. It takes a signal from the RoboRIO and translates it into the power that makes the motor spin.

Some motors include a motor controller built in- for example, the drivetrain motors.

For the other motors, we use a Spark Max controller.

Each type of controller needs its own control classes.

## Your First Motor Subsystem

Let's create a simple subsystem to control a single motor. This is for a motor controlled by a Spark Max.

```java
// ... skip imports ...
public class MotorSubsystem extends SubsystemBase {
    private final CANSparkMax motor = new CANSparkMax(Constants.MOTOR_ID, MotorType.kBrushless);

    private void set(LinearVelocity speed) {
        if (speed.compareTo(MotorConstants.MAX_SPEED) > 0) {
            return;
        }

        motor.set(MetersPerSecond.div(MotorConstants.MAX_SPEED).in(Value));
    }

    public Command getSetSpeed(LinearVelocity speed) {
        // Runs the first lambda when the Command is started and the second when it's ended.
        return startEnd(() -> set(speed), () -> set(MetersPerSecond.zero()));
    }
}
```

* We have a `CANSparkMax` member object declared called `motor`. It's defined to represent our specific motor.
* The `setSpeed()` method takes a `double` between -1.0 and 1.0 and sets that to be the speed of the motor.
    - It could alternatively be a setVoltage (with Voltage and Volts replacing LinearVelocity and MetersPerSecond).
* `getSetSpeed()` gets (returns) a command that sets the speed to the passed value.
    - For example, you could have this code in your RobotContainer:
```java
// as an instance variable
private static final MotorSubsystem motor = new MotorSubsystem();

// in configureBindings (or RobotContainer())
driveController.a().whileTrue(motor.getSetSpeed(MetersPerSecond.of(0.5)));
```
    - This will bind the a button on the controller to move the motor at 0.5 m/s while pressed and then stop it on release.

## Encoders

Most of the motors and controllers we use have a built-in encoder. An encoder is a sensor that tells us how far the motor has spun.

Let's add a method to our subsystem to read the encoder position:

```java
// ... inside the MotorSubsystem class ...

public double getPosition() {
    return motor.getEncoder().getPosition();
}
```

This method returns the position of the motor in rotations. We can also get the velocity of the motor in RPM (rotations per minute):

```java
// ... inside the MotorSubsystem class ...

public double getVelocity() {
    return motor.getEncoder().getVelocity();
}
```

## Hitting the Reset Button

Sometimes, we need to reset the encoder to zero. For example, we might want to do this when our arm is in its home position. We can add a method to our subsystem to do this:

```java
// ... inside the MotorSubsystem class ...

public void resetEncoder() {
    motor.getEncoder().setPosition(0);
}
```

## Let's Get Building!

Now that you know the basics of motor control, it's time to put your knowledge to the test. In the next lesson, we'll learn how to get input from the world around us using sensors.
