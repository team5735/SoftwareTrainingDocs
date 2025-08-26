# Intro to Software

Welcome to the Software subteam in the Control Freaks. This'll be a short first lesson to get you into the world of software.

Think of software as the robot's nervous system. It's the code that:

* **Gathers information** from sensors.
* **Makes decisions** based on that information.
* **Sends commands** to the motors and other moving parts.

### What Language Do We Speak?

Inside every FRC robot is a computer called the **RoboRIO** made specifically for this competition. Our job is naturally to write code that will run on that computer.

The FRC community has created a fantastic set of tools called **WPILib** that makes writing robot code much easier. WPILib officially supports three languages:

* C++
* Java
* Python

Here on the Control Freaks, we use **Java**, because it's taught in APCSA at WHS, making it accessible to many students. But don't worry if you've never written a line of Java in your life! We'll teach you everything you need to know in lesson 002 (the third one), after setup.

### How We Structure Our Code

We use a "Command-based" programming model. It sounds fancy, but the idea is simple:

* **Subsystems:** We break the robot down into its physical parts in the code. The drivetrain, the shooter, the climber – each of these is a **subsystem**.
* **Commands:** A **command** is a specific action that a subsystem can perform. For example, the shooter subsystem might have a "shoot" command, and the drivetrain might have a "drive forward" command.

With this structure, our code directly represents the robot and its behaviour, which makes the code much easier to write and think about.

## The Software Subteam

Our job is to write this code. Ideally, we work closely with the people in the other room who chose mechanical, so that they don't build something we can't code and so that our code makes sense with the pile of metal they've built.

Ok, that's it for this lesson. I know you were all thoroughly excited for a full lecture, but those days are coming later. I hope you stick with us.

These lessons are all available online: `https://github.com/team5735/SoftwareTrainingDocs`

If you'd like to save that link, you can type it into your browser right now and bookmark it.

To find the lesson documents themselves, go to the lessons folder and click on any file.
