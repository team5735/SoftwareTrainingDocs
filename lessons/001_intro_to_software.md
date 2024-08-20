# INTRO TO SOFTWARE

[//]: # "This is less so a lesson and more of a presentation. The hope is to give this one in one of the first meetings, to give an overview of software. This presentation should take approx. 15-30 minutes."

## Opening

When thinking of a robot, the physical form is often what comes to mind,
yet for any practical projects, a union of two equally complex fields must
be made:

1. mechanics, the tangible body of any project
2. software, the deep running nervous system of a robot

Software is responsible for moving data to and from different core parts
within the robot, analyzing that data, and using the results of that
analysis to execute actions.

We hope that, by the end of this presentation:
- we will properly convey the basics of robot code and why it matters
- all members of the Control Freaks will understand the Software subteam
and its workflows
- we will garner interest in members potentially joining the Software
subteam

## The Code

### Languages

Within all FRC robots is a component called a RoboRIO. It is a processor with
wires that run to all subsystems of the robot, acting as the information hub by
taking feedback from each component and sending back commands. 

The task then, of Software, is to tap into this flow, to give the RoboRIO, and
thus each subsystem, commands, and to utilize the data coming from different
sensors. To interface with the RoboRIO, or simply the robot as a whole,
requires writing and providing code to be used during operation.

When coding the robot, tools are provided by FIRST to make it easier,
allowing for quick exporting to the RoboRIO. These tools are called WPILib
and officially support three programming languages, as of 2024. These
languages are:

- C++
- Java
- Python

On the Control Freaks' Software team, we choose to use Java, placing us
within the majority of FRC teams. We use Java, though it may be slower at
times, primarily because it is the most accessible here at WPI. Many
students have taken or are going to take the AP Computer Science A class,
thus learning Java, and, for those who have not, there are numerous online
resources through which to easily learn. The intention is that minimal
experience will be necessary for any new Software members.

### Architecture

WPILib uses a "Command-based" structure. This means that every action to be
carried out by the Robot should be defined by an relative Command object within
the code. These Commands are then queued up and run every 20 milliseconds by an
internal process called the Command Scheduler. Commands can be tied to Triggers
such as button presses from our Driver's controller, or activated specifically
within the code.

A Command may require a given subsystem, those being another core pillar of our
codebase. The base definition of a subsystem hopefully self-explanatory. It is
smaller system contained within a larger system, a sub-system. Often subsystems
are physically defined, being modular structures built by Mechanical to be
placed onto the robot. Within Software, we also have subsystems, though within
the code, usually reflecting a physical structure.

A coded Subsystem is often defined as containing electrical components that
only it is intended to access. Frequently these components are motors or
sensors, though Subsystems can represent things less tangible such as lighting
or vision. Any component with logic behind it will have a relevant Subsystem.
Within the code for each subsystem we will typically define a set of useable
Commands for that Subsystem, gating access of the inner components except for
through these Commands. Only one Command can ever require a given Subsystem, to
run another with the same Subsystem would require ending the previous Command. 

It is through these self-imposed restrictions that we are able to construct a
robot with minimal potential for error, that we are able to more efficiently
consider whence problems may arise.
