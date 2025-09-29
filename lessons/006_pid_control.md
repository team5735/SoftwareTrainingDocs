# PID Control

> This lesson will introduce the concept of PID control, a fundamental algorithm in robotics.

## Introduction

So far, we've been controlling our motors by setting their speed to a value between -1.0 and 1.0. This is called open-loop control, because we are not using any feedback from the motor to adjust the speed. This works for simple tasks, but for more precise control, we need to use closed-loop control.

Closed-loop control is where we use feedback from a sensor to adjust the output to our motor. The most common form of closed-loop control in FRC is PID control.

## What is PID?

PID stands for Proportional, Integral, and Derivative. It is a control algorithm that uses feedback from a sensor to calculate the output to a motor. The goal of PID control is to get the sensor reading to match a desired setpoint.

Let's break down the three parts of PID:

* **Proportional (P)**: The P term is proportional to the error, which is the difference between the setpoint and the current sensor reading. The larger the error, the larger the P term. This is the main driving force of the PID controller.
* **Integral (I)**: The I term is proportional to the accumulated error over time. The I term is used to correct for small, steady-state errors that the P term alone cannot fix.
* **Derivative (D)**: The D term is proportional to the rate of change of the error. The D term is used to dampen the response of the PID controller and prevent it from overshooting the setpoint.

By tuning the three constants (kP, kI, and kD), we can create a PID controller that is fast, accurate, and stable.

## Implementing PID Control

WPILib provides a `PIDController` class that makes it easy to implement PID control. We can use this class in our subsystems to control the position of our mechanisms.

Let's add a PID controller to our `MotorSubsystem` from the previous lesson.

```java
// ... inside the MotorSubsystem class ...

private final PIDController pidController = new PIDController(Constants.kP, Constants.kI, Constants.kD);

public void setSetpoint(double setpoint) {
    pidController.setSetpoint(setpoint);
}

public void usePID() {
    double output = pidController.calculate(getEncoder().getPosition());
    motor.set(output);
}
```

In this example, we've created a `PIDController` with the constants from our `Constants.java` file. We've also added a `setSetpoint` method to set the desired position of the motor. Finally, we've added a `usePID` method that calculates the output of the PID controller and sets the speed of the motor. This method would be called in a command.

## Tuning PID Controllers

Tuning a PID controller is the process of finding the right values for kP, kI, and kD. This is often a process of trial and error. Here's a general procedure for tuning a PID controller:

1.  Set kI and kD to zero.
2.  Increase kP until the mechanism starts to oscillate (shake back and forth) around the setpoint.
3.  Reduce kP by a small amount.
4.  Increase kD to reduce the overshoot and dampen the oscillation.
5.  If there is a small, steady-state error, increase kI to correct for it.

WPILib provides tools like the SmartDashboard and Shuffleboard that allow you to tune PID controllers in real-time, without having to redeploy your code.

## Conclusion

In this lesson, we've learned about PID control, a fundamental concept in robotics. We've seen how to implement a PID controller using WPILib and how to tune it. With PID control, we can create mechanisms that are fast, accurate, and reliable.