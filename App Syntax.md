# Runner Script Syntax

A minimal line-based scripting language executed by the Runner class to control events, messages, items, and timing across experiences.

Rules:
- Commands are case-sensitive
- Strings must use double quotes
- Lines execute top to bottom
- Invalid commands stop execution immediately

Variables:
define <name> = <value>
Examples:
define count = 3
define title = "Happy Hour"

Values auto-resolve as numbers, strings, or variables. Variables can be reused later in the script.

String Expressions:
String concatenation uses ..
Unknown variables resolve to an empty string.
Example:
print "Hello " .. title

Commands:

print <expression>
Outputs text to the console/log.

wait <seconds>
Pauses execution for the given number of seconds.

version or v
Prints the current runner version.

item <Egg | Crate | All> [amount]
Spawns admin items in the map.
If amount is omitted, defaults to 1.
All spawns both AdminEgg and AdminCrate.

message <expression> [userId]
Posts a global message across experiences.
userId is optional and must resolve to a number.

admin "<eventName>"
Starts an admin event with the given name.

admin end "<eventName>"
Ends the specified admin event.

happyhour "<message>" <color> <durationSeconds> [options]
Starts a happy hour event.
Supported options:
priceset:<number>
pricepercentage:<number>

happyhour end
Ends the active happy hour.

Loops:
loop for <count>; <var> {
  <commands>
}
Runs the block count times.
The loop variable starts at 1 and increments each iteration.

Example Script:
define title = "Weekend Event"
message "Starting " .. title
admin "Weekend Event"
loop for 2; i {
  item Egg
  wait 2
}
happyhour "LIMITED TIME!" Gold 300 pricepercentage:20
wait 10
happyhour end
admin end "Weekend Event"

Errors:
Unknown or invalid command: <line>
Execution stops immediately when an error occurs.

Version:
v14025.50 (beta)
