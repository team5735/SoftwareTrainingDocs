# INTRO TO SOFTWARE

> This is less so a lesson and more of a presentation. The hope is to give this one in one of the first meetings, to give an overview of software.

## Opening

When thinking of a robot, the physical form is often what comes to mind, yet for any practical projects, two equally complex fields must be brought together:

1. mechanics, the tactile body of any project
2. software, the nervous system of the robot

Software is responsible for moving data to and from different core parts within the robot, analyzing that data, and using the results of that analysis to perform tasks.

We hope that, by the end of this presentation:
- you will understand the basics of robot code and why it matters
- you will understand the software subteam and its workflows
- some of you will feel a bit of interest in joining Software

## The Code

### Languages

Within all FRC robots is a component called a RoboRIO. It is a processor with wires that run to all subsystems of the robot, acting as the information hub by taking feedback from each component and sending back commands. 

The goal of software is to tap into this flow, writing code for the RoboRIO to run, and to utilize the data coming from different sensors. To talk to the RoboRIO, or simply the robot as a whole, requires writing and providing code to be executed when running the robot.

The FRC community has developed a set of tools and libraries for robot programming, allowing for quick development. These tools and libraries are called WPILib and officially support three programming languages, namely:

- C++
- Java
- Python

On the Control Freaks' Software team, we choose to use Java, as do the majority of software teams. The main reason for this choice is its accessibility at WHS, considering it's taught in APCSA, or at least easy for those who want to learn seperately, easy to learn. The intention is that no minimal experience will be necessary for any new Software members.

### Architecture

WPILib uses a "Command-based" structure. This means that every action for the Robot should be defined by a Command object within the code. Commands can be tied to Triggers such as button presses from our Driver's controller, or activated manually within the code.

A Command may "require" a given subsystem, which is another large part of this framework. A subsystem corresponds to, well, a physical subsystem on the robot. Often subsystems are physically defined, being modular parts of the robot, built by Mechanical. Within Software, we also create subsystems, though within the code, usually to reflect such a physical structure.

A coded Subsystem is often defined as owning electrical components that only it is intended to use. Frequently these components are motors or sensors, though Subsystems can represent abstract things such as lighting or vision. Any component with logic behind it will have a relevant Subsystem. Within the code for each subsystem we will typically define a set of Commands for that Subsystem, gating access of the inner components except for through these Commands. Only one Command can ever require a given Subsystem, to run another with the same Subsystem would require ending the previous Command. 

It is through these self-imposed restrictions of Command-Based that we are able to construct a robot with minimal potential for error, that we are able to more efficiently consider whence problems may arise.

## The Subteam

Almost every FRC team has some aspect of software. Whether an entire subteam, a few dedicated members, or simply one specialist, there must be a way for the team to code their robot. On the Control Freaks, we define Software as a subteam, with a separate knowledge base and training system from Mechanical or Electrical.

Every year for Software has been an uphill battle against disorganization (as most things are), and this year we hope to make monumental progress in said fight. Software will begin on the 21st, splitting off for a series of lessons intended to thoroughly explain the various systems in the Robot and how we use them, before rejoining for  offseason projects, hopefully around the same time Mechanical/Electrical training ends.

When working on projects, the hope is to have a less subteam-oriented process, instead having Software members work alongside specific groups on subsystems and other robot parts. Software would still meet for brief stand-up meetings about once  a week, possibly more frequently during practice, to discuss issues and share progress. The overall intent is to completely reintegrate Software members after training, to prevent the subteam divide that has been present in the past.

## Outro

The environment of Software this year is intended to be more individual-oriented, while still being one where collaboration is welcome when help is needed. Software will always be an iterative process, and criticism is always welcome.

Software training will begin soon, and we hope to see some of you there; it takes a smidge more ambition than mechanical. All jokes aside though, make whatever choice makes you most happy, for anything involving robotics can beget a strong and successful career.

Thank you all so much for listening to this exposition, any questions are welcome, though I expect mechanical is itching to start today's activity.
