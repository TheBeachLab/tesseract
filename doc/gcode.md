# Gcode Reference
Some of the more complicated commands are described here. Much of this is shamelessly cribbed from the [LinuxCNC Gcode pages](http://www.linuxcnc.org/docs/2.4/html/gcode_main.html)<br>

## G10 Set Parameters (Offsets)
Currently the only G10 command supported is G10 L2, which is used to set coordinate offsets. Use Pn to select coordinate system 1-6 (G54 - G59, respectively), and one or more axis value to set the offset for that axis. The format is:
<pre>
G10 L2 P1 X0 Y0 Z0 A0 B0 C0  - set G54 offsets to zero, making G54 act as persistent absolute coordinates
</pre>

## G28, G28.1, G30, G30.1 Go To Predefined Position
G28 (and G30) will move the machine to the absolute coordinates set in G28.1 (G30.1), optionally through an intermediate point.  Movement will occur at the traverse rate (G0 rate). Axes that are not specified are ignored (not moved). The axis value is the intermediate point for that axis.

Format is:
<pre>G28 X0 Y0 Z0 A0 B0 C0</pre>

Gcode | Parameters | Command | Description
------|------------|---------|-------------
G28 | _axes_ | Go to G28.1 position | Goes through intermediate point if _axes_ are present
G28.1 | | Set position for G28 | Axes are not used and are ignored if present
G30 | _axes_ | Go to G30.1 position | Goes through intermediate point if _axes_ are present
G30.1 | | Set position for G30 | Axes are not used and are ignored if present

Example of use:
* Go to an arbitrary position, e.g. G0 x100 y100
* Send G28.1  - This will "remember" the absolute position. This position remains constant regardless of what coordinate system is in effect.
* Then go to a different place, e.g. G0 x50 y50
* Send G28  - The machine will return to x100 y100

Example:
* Go back to X0Y0
* Send G91 G28 Z10 - this will move to x100 y100. The tool will initially lift z by 10 mm (or inches); G91 is used to set relative mode for this command.

## G61, G61.1, G64 Path Control Modes
TinyG supports exact path mode (G61) and exact stop mode (G61.1). G64 is recognized, but is treated as exact path mode. In exact stop mode motion will stop between each Gcode block. In exact path mode the exact path is followed (i.e. corners are not rounded). The velocity at the points joining 2 blocks is controlled to keep the change in direction between the blocks within centripetal acceleration limit set by $JA. Please see [here](https://github.com/synthetos/TinyG/wiki/Configuration#xjd---junction-deviation) for an explanation.

## M2, M30 Program End
program END (M2, M30) performs the following actions:

* Axis offsets are set to G92.1 CANCEL offsets
* Set default coordinate system (uses $gco)
* Selected plane is set to default plane ($gpl)
* Distance mode is set to MODE_ABSOLUTE (like G90)
* Feed rate mode is set to UNITS_PER_MINUTE (like G94)
* The spindle is stopped (like M5)
* Motion mode is canceled like G80 (not set to G1)
* Coolant is turned off (like M9)
* Default INCHES or MM units mode is restored ($gun)

## Gcode Comments
 * Comments start with a '(' char or alternately a semicolon ';'
 * Comments always terminate the block - i.e. leading or embedded comments are not supported
<pre>
Valid comment cases       Notes:
G0X10                      - command only - no comment
G0X10 (comment text)       - command with comment
G0X10 (comment text        - it's OK to drop the trailing paren
G0X10 ;comment text        - comment delimited by semicolon (firmware build 378.05 and later)
(comment text)             - there is no command on this line
</pre>
<pre>
Invalid comment cases     Notes:
G0X10 comment text         - comment with no separator
N10 (comment) G0X10        - embedded comment. G0X10 will be ignored
(comment) G0X10            - leading comment. G0X10 will be ignored
G0X10 #comment             - invalid comment separator
</pre>