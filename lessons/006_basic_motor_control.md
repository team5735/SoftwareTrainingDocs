# Motors: Making Things Move

> This is where the fun begins! In this lesson, we'll learn how to control motors, the muscles of our robot. This will be a hands-on lesson, so get ready to make some sparks fly (not literally, of course).

## The Brains Behind the Brawn

To control a motor, we need a **motor controller**. This is a small electronic device that sits between the RoboRIO and the motor. It takes a signal from the RoboRIO and translates it into the power that makes the motor spin.

On our team, we use the **REV Robotics SPARK MAX** motor controller. It's a powerful and versatile controller that's perfect for FRC.

## Your First Motor Subsystem

Let's create a simple subsystem to control a single motor. As we learned in the last lesson, a subsystem is a class that represents a part of the robot. Here's what a basic motor subsystem looks like:

```java
package frc.robot.subsystems;

import com.revrobotics.CANSparkMax;
import com.revrobotics.CANSparkMaxLowLevel.MotorType;

import edu.wpi.first.wpilibj2.command.SubsystemBase;
import frc.robot.Constants;

public class MotorSubsystem extends SubsystemBase {
    private final CANSparkMax motor;

    public MotorSubsystem() {
        motor = new CANSparkMax(Constants.MOTOR_ID, MotorType.kBrushless);
    }

    public void setSpeed(double speed) {
        motor.set(speed);
    }
}
```

Let's break this down:

* We have a `CANSparkMax` object called `motor`.
* In the constructor, we create a new `CANSparkMax` object and give it the CAN ID from our `Constants.java` file.
* The `setSpeed()` method takes a `double` between -1.0 and 1.0 and sets the speed of the motor.

## Encoders: The Motor's Sixth Sense

Most of the motors we use have a built-in **encoder**. An encoder is a sensor that tells us how far the motor has spun. This is incredibly useful for controlling the position of our mechanisms.

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