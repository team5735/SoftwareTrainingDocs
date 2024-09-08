# Style

No m_ prefix.
Constants are SCREAMING_SNAKE_CASE.
... and don't prefix constant names with their subsystem (unless they're in the main Constants.java).
Use camelCase for methods and members, CamelCase for classes.
Use factory commands if reasonable: e.g. upStopCommand Longer, more sophisticated commands go in their own class.
Don't prefix commands with their subsystem (but do use a Command suffix.
Separate constants files.
Formatting: use clang-format! its .clang-format file defined in the repo.
Commented code stinks.
Use DoubleSections and BooleanSections and TunableNumbers and and and...
Use "topic" branches, have a trunk dev branch, and main is a release/stable/competition branch.
Put the unit of a variable in its name.
Prefer degrees to radians.
For publishers in double/boolean sections, include the units at all times, replacing words like "speed", and be verbose.
Code reviews are perfomed on every attempted merge, and are discussed in person, if possible.

## Unit suffixes
Assume SI units unless specified otherwise (e.g., meters for distance/positions)
Put an underscore and then the unit:
- sec
- mps "m/s"
- mms "mm/s"
- met
- volts
- amps
- deg
- rad if necessary
- rot "device rotations"
- gram

# Organization
Standups start off every meeting.
Every now and then (TBD) we have  a longer meeting covering everything.
