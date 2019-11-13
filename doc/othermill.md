# Othermill CNC

## Full TinyG G-Code specifications

This table summarizes Gcode supported. _axes_ means one or more of X,Y,Z,A,B,C.

Gcode | Parameters | Command | Description
------|------------|---------|-------------
G0 | _axes_ | Straight traverse | Traverse at maximum velocity. At least one axis must be present
G1 | _axes_, F | Straight feed | Feed at feed rate F. At least one axis must be present
G2 | _axes_, F, I,J,K or R | Clockwise arc feed | Arc at feed rate F. Offset mode IJK or radius mode R
G3 | _axes_, F, I,J,K or R | Counter clockwise arc feed | Arc at feed rate F. Offset mode IJK or radius mode R
G4 | P | Dwell | Pause for P seconds
[G10 L2](#g10-set-parameters-offsets) | _axes_, P | Set offset parameters | P selects coordinate system 1-6
G17 | | Select XY plane | G17, G18 and G19 set the plan in which the G2/G3 arcs are drawn
G18 | | Select XZ plane |
G19 | | Select YZ plane |
[G20](Inch-and-Millimeter-Units-Mode) | | Select inches units mode | All Gcode from this point on will be interpreted in inches
[G21](Inch-and-Millimeter-Units-Mode) | | Select mm units mode | All Gcode from this point on will be interpreted in millimeters
[G28](#g28-g281-g30-g301-go-to-predefined-position) | _axes_ | Go to G28.1 position | Optional axes specify an intermediate point
[G28.1](#g28-g281-g30-g301-go-to-predefined-position) | | Set position for G28 | The current machine position is recorded (No parameters are provided)
[G28.2](https://github.com/synthetos/TinyG/wiki/Homing-and-Limits-Description-and-Operation#g282---homing-sequence-homing-cycle) | _axes_ | Homing Sequence | Homes all axes present in command. At least one axis must be specified
[G28.3](https://github.com/synthetos/TinyG/wiki/Homing-and-Limits-Description-and-Operation#g283---set-absolute-position) | _axes_ | Set Absolute Position | Set axis to zero or other value. Use to zero axes that cannot otherwise be homed
[G30](#g28-g281-g30-g301-go-to-predefined-position) | _axes_ | Go to G30.1 position | Optional axes specify an intermediate point
[G30.1](#g28-g281-g30-g301-go-to-predefined-position) | | Set position for G30 | The current machine position is recorded (No parameters are provided)
G53 | | Select absolute coordinates | Non-Modal: Applies only to current block
G54 | | Select coord system 1 | G54 is typically used as the "normal" coordinate system and reflects the machine position
G55 | | Select coord system 2 |
G56 | | Select coord system 3 |
G57 | | Select coord system 4 |
G58 | | Select coord system 5 |
G59 | | Select coord system 6 |
[G61](#g61-g611-g64-path-control-modes) | | Exact path mode | Continuous motion between Gcode blocks - exact path will be traced - stops only if it must
[G61.1](#g61-g611-g64-path-control-modes) | | Exact stop mode | Motion will stop between each Gcode block
[G64](#g61-g611-g64-path-control-modes) | | Continuous path mode | Sacrifice path following accuracy in order to keep the feed rate up
G80 | | Cancel motion mode |
G90 | | Set absolute mode |
G91 | | Set incremental mode |
G92 | _axes_ | Set origin offsets |
G92.1 | | Reset origin offsets |
G92.2 | | Suspend origin offsets |
G92.3 | | Resume origin offsets |
G93 | | Set inverse feedrate mode |
G94 | | Cancel inverse feedrate mode |

 Mcode | Parameter |Command | Description
------|-----------|--------|-------------
M0 | | Program stop |
M1 | | Program stop | Optional program stop switch is not implemented so M1 is equivalent to M0
[M2](#m2-m30-program-end) | | Program end |
[M30](#m2-m30-program-end) | | Program end |
M60 | | Program stop |
M3 | S | Spindle on - CW | S is speed in RPM
M4 | S | Spindle on - CCW | S is speed in RPM
M5 | | Spindle off |
M6 | | Change tool | No operation at this time
M7 | | Mist coolant on | Note that mist and flood share the same Coolant ON/OFF pin
M8 | | Flood coolant on | Note that mist and flood share the same Coolant ON/OFF pin
M9 | | All coolant off | Note that mist and flood share the same Coolant ON/OFF pin

 Other | Parameter |Command | Description
------|-----------|--------|-------------
N | line number | label gcode block | Line numbers are allowed, handled, and may be reported back in status reports. Don't underestimate how useful this is for debugging Gcode files.
[()](#gcode-comments) | [comment](#gcode-comments) | [gcode comment](#gcode-comments) | Gcode comments are supported. They are stripped and ignored, except for messages (below)
[;](#gcode-comments) | comment | alternate comment | A semicolon is an alternate way to delimit a comment. This is not Gcode "standard", but is used by Mach and some Reprap codes. (available as of build 378.05)
(msg....) | message | gcode message | Gcode messages are comments that begin with the characters `msg` (case insensitive). These will be echoed to the operator

## G-Code Not supported by the Othermill

Commands the milling machine does not support

The following commands are either not supported by TinyG, or supported by TinyG but not supported by th emilling machine or software. Files that contain unsupported commands may be unable to load, or lines containing unsupported commands may be skipped. If you find that you can’t import your file, or odd things happen like the spindle doesn’t turn on, check your file to see if it contains the following commands.

Command 	Name 	Description
G81-G85 	Canned cycles 	A “canned cycle” is a way of performing repetitive machining functions like making holes or slots. A common one is G85, which is the “mill slot” command. It’s often used in g-code generated by PCB design software. TinyG (and thus the milling machine) doesn’t support this command, so files that contain it can’t be loaded. A workaround is to make a row of overlapping holes instead of a slot.
G54, G56, G57, G58, G59 	Alternate coordinate systems 	Coordinate systems other than G55 are not supported by the software, so make sure you use G55. In some cases, if your software uses a different coordinate system, manually editing the g-code file and changing the command (i.e. from G54 to G55) will make your file work properly.
G18 	Select XZ plane 	An uncommon command, but occasionally used by CAM software. There is a TinyG firmware bug that causes XZ arcs to be be interpreted incorrectly. We are working to fix this issue in future firmware versions.
G93 	Set inverse feedrate mode 	There is a TinyG firmware bug that either cancels the command as soon as you enter any other command, or causes older TinyGs to crash.
E 	Fixturing offset 	Some CAM software will try to use the E command to set a fixturing offset, but this causes the software to ignore the entire line containing the E command.
G40-G51 	Tool compensation 	Some CNC machines use commands for specifying tool compensation, but TinyG does not recognize those commands.
M4 	Spindle on - CCW 	Not supported by milling machine spindle - it only turns clockwise
M7 	Mist coolant on 	The milling machine is not equipped with coolant
M8 	Flood coolant on 	The milling machine is not equipped with coolant
M9 	All coolant off 	The milling machine is not equipped with coolant