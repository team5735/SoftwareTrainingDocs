# Sensors and Input: Giving Your Robot Senses

> In the last lesson, we learned how to make our robot move. But a robot isn't much good if it can't see or hear what's going on around it! In this lesson, we'll learn how to give our robot senses using various sensors and how to take commands from a driver.

## The Driver's Seat: Your Controller

During the teleoperated period of a match, you'll be controlling the robot with an Xbox controller. This is your primary way of telling the robot what to do. The Xbox controller has a bunch of buttons, triggers, and joysticks, and we can use all of them to control our robot.

In `RobotContainer.java`, we can create an instance of the `CommandXboxController` class to represent our controller:

```java
// ... inside the RobotContainer class ...

private final CommandXboxController driverController = new CommandXboxController(Constants.DRIVER_CONTROLLER_PORT);
```

Once you have your controller object, you can easily get input from it:

```java
// Get the value of the left joystick's Y axis
double leftY = driverController.getLeftY();

// Check if the A button is pressed
boolean aButtonPressed = driverController.a().getAsBoolean();
```

Even cooler, you can directly link a button press to a command:

```java
// ... in the RobotContainer constructor ...

driverController.a().onTrue(new MyCommand());
```

This line of code will automatically schedule `MyCommand` to run as soon as the A button is pressed. Pretty neat, right?

## Sensors: The Robot's Eyes and Ears

Sensors are how our robot perceives the world around it. There are many different types of sensors, but here are a few common ones you'll encounter:

* **Encoders**: We've already met these! They tell us how much a motor has rotated.
* **Gyroscopes**: A gyroscope measures rotation. We use it to know which way our robot is facing and to help it drive straight.
* **Limit Switches**: These are simple on/off switches. They're great for detecting when a mechanism has reached its end point, like an arm fully extended or retracted.
* **Cameras**: We use cameras for vision processing, like identifying game pieces or aligning with targets on the field.

### Gyroscopes: Keeping Your Robot Straight

Knowing your robot's heading is super important, especially for autonomous routines. We often use an ADXRS450 gyro, which connects to the RoboRIO.

Here's how you might set one up in your drivetrain subsystem:

```java
// ... inside the DrivetrainSubsystem class ...

private final ADXRS450_Gyro gyro = new ADXRS450_Gyro();

public double getHeading() {
    return gyro.getAngle();
}

public void resetHeading() {
    gyro.reset();
}
```

### Limit Switches: Knowing Your Limits

A limit switch is a simple digital sensor. It's either pressed (closed) or not pressed (open). You can read its state like this:

```java
// ... inside a subsystem ...

private final DigitalInput limitSwitch = new DigitalInput(Constants.LIMIT_SWITCH_PORT);

public boolean isLimitSwitchPressed() {
    // The get() method returns true when the switch is open, so we invert it.
    return !limitSwitch.get();
}
```

## Putting It All Together

By combining motor control with sensor input and driver commands, you can start to build a truly interactive and responsive robot. This is where the real fun of robot programming begins!