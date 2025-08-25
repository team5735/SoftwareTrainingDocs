# Java code style
No m_ prefix for member variables.
Use camelCase for non-types; PascalCase for types.
Put the unit of a variable in its name.
Prefer degrees to radians.

Constants are SCREAMING_SNAKE_CASE, and not prefixed with their subsystem.
Separate constants files.

Use factory commands if reasonable (methods that return a command).
Longer, more sophisticated commands go in their own class.
Suffix command classes with Command.

For formatting, if you have clang-format installed you can run `clang-format -i src/**/*.java`.
Instead of commenting code, prefer using git history.

Use the classes in utils.
For publishers in double/boolean sections, include the units at all times, replacing words like "speed", and be verbose (spaces are ok).

Use "topic" branches, have a trunk dev branch, and main is a stable competition branch.
Code reviews are perfomed on every attempted merge, and are discussed in person, if possible.

## Unit suffixes
Assume SI units unless specified otherwise (e.g., meters for distance/positions)
Put an underscore and then the unit:
- s/sec
- mps = m/s
- mms = mm/s
- m/met
- v/volts
- A/amps
- deg
- rad if necessary
- rot = device rotations
- g/gram
