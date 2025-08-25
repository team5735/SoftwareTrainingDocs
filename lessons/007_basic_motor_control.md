# Basic Motor Control

> This lesson will be very hands-on. The goal is to get everyone comfortable with controlling motors and reading from the encoders.

## Introduction

Motors are the muscles of our robot. They are what allow us to drive, shoot, and manipulate game pieces. In this lesson, we'll learn how to control motors using WPILib.

## Motor Controllers

To control a motor, we need a motor controller. A motor controller is a small electronic device that takes a signal from the RoboRIO and uses it to control the speed and direction of a motor. There are several different types of motor controllers that are legal for FRC use, but on our team, we primarily use the REV Robotics SPARK MAX.

## Creating a Motor Subsystem

As we learned in the previous lesson, we use subsystems to organize our code. Let's create a simple subsystem for a single motor.

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

In this subsystem, we have a single `CANSparkMax` motor controller. The constructor initializes the motor with the CAN ID from our `Constants.java` file. The `setSpeed` method sets the speed of the motor. The speed is a value between -1.0 and 1.0, where 1.0 is full speed forward and -1.0 is full speed reverse.

## Reading from Encoders

Most motors that we use in FRC have built-in encoders. An encoder is a sensor that measures the rotation of the motor shaft. This is incredibly useful for controlling the position of our mechanisms.

Let's add a method to our `MotorSubsystem` to read the encoder position.

```java
// ... inside the MotorSubsystem class ...

public double getPosition() {
    return motor.getEncoder().getPosition();
}
```

The `getPosition()` method returns the position of the motor in rotations. We can also get the velocity of the motor in RPM (rotations per minute).

```java
// ... inside the MotorSubsystem class ...

public double getVelocity() {
    return motor.getEncoder().getVelocity();
}
```

## Resetting the Encoder

Sometimes, we need to reset the encoder to zero. For example, we might want to reset the encoder on our arm mechanism when it is at its home position. We can do this by adding a method to our subsystem.

```java
// ... inside the MotorSubsystem class ...

public void resetEncoder() {
    motor.getEncoder().setPosition(0);
}
```

## Conclusion

In this lesson, we've learned how to control motors and read from encoders. We've also seen how to create a simple motor subsystem. In the next lesson, we'll learn how to use sensors to get input from the world around us.