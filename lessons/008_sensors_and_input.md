# Sensors and Input

> This lesson will cover how to get input from various sensors and from the driver's controller.

## Introduction

In the last lesson, we learned how to control motors. But a robot is more than just a collection of motors. We also need to be able to sense the world around us and get input from the driver. In this lesson, we'll learn how to use sensors and get input from the driver's controller.

## The Driver's Controller

The driver's controller is our primary source of input during the teleoperated period. We use an Xbox controller, which has a variety of buttons, triggers, and joysticks. We can use these inputs to control the robot.

In `RobotContainer.java`, we can create an instance of the `CommandXboxController` class to represent our controller.

```java
// ... inside the RobotContainer class ...

private final CommandXboxController driverController = new CommandXboxController(Constants.DRIVER_CONTROLLER_PORT);
```

Once we have our controller object, we can use it to get the state of the buttons, triggers, and joysticks.

```java
// Get the value of the left joystick's Y axis
double leftY = driverController.getLeftY();

// Get the state of the A button
boolean aButtonPressed = driverController.a().getAsBoolean();
```

We can also use the controller to trigger commands. For example, we can run a command when a button is pressed.

```java
// ... in the RobotContainer constructor ...

driverController.a().onTrue(new MyCommand());
```

This will schedule `MyCommand` when the A button is pressed.

## Sensors

Sensors are what allow our robot to perceive the world. There are many different types of sensors that we can use in FRC, but some of the most common are:

*   **Encoders**: We learned about these in the last lesson. They measure the rotation of a motor shaft.
*   **Gyroscopes**: A gyroscope measures the rate of rotation. We use a gyro to keep the robot driving straight.
*   **Limit Switches**: A limit switch is a simple switch that is triggered when it comes into contact with something. We use limit switches to detect when a mechanism has reached the end of its travel.
*   **Cameras**: We use cameras to see the field and to help us align with game pieces and targets.

### Gyroscopes

We use a gyroscope to measure the robot's heading. This is essential for driving straight in autonomous mode. We use the ADXRS450 gyro, which is a small sensor that connects to the RoboRIO's SPI port.

Here's how you can create a gyro object in your drivetrain subsystem:

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

### Limit Switches

A limit switch is a digital input. It is either open or closed. We can create a `DigitalInput` object to represent a limit switch.

```java
// ... inside a subsystem ...

private final DigitalInput limitSwitch = new DigitalInput(Constants.LIMIT_SWITCH_PORT);

public boolean isLimitSwitchPressed() {
    // The get() method returns true when the switch is open, so we invert it.
    return !limitSwitch.get();
}
```

## Conclusion

In this lesson, we've learned how to get input from the driver's controller and from various sensors. This is a crucial part of writing robot code, as it allows us to make our robot interactive and responsive to its environment.