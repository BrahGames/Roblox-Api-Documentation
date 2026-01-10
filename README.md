# Runner Script Syntax

A minimal line-based scripting language executed by the Runner class to control events, messages, items, and timing across experiences.

**Rules**
- Commands are case-sensitive
- Strings must use double quotes
- Lines execute top to bottom
- Invalid commands stop execution immediately

**Variables**
define <name> = <value>
Examples:
define count = 3
define title = "Happy Hour"

Values automatically resolve as numbers, strings, or variables. Variables can be reused later in the script.

**String Expressions**
String concatenation uses ..
Unknown variables resolve to an empty string.
Example:
print "Hello " .. title

**Commands**

**print**
Syntax: print <expression>

**wait**
Syntax: wait <seconds>

**version / v**
Syntax: version
Syntax: v

**item**
Syntax: item <ItemName> [amount?]
ItemName options: Egg | Crate | All
amount? = optional integer (defaults to 1)

**message**
Syntax: message <expression> [userId?]
userId? = optional number

**admin**
Syntax: admin "<eventName>"

**admin end**
Syntax: admin end "<eventName>"

**happyhour**
Syntax: happyhour "<message>" <color> <durationSeconds> [priceset:<number>?] [pricepercentage:<number>?]

priceset? = optional fixed price
pricepercentage? = optional percentage discount

**happyhour end**
Syntax: happyhour end

**Loops**
Syntax:
loop for <count>; <varName> {
  <commands>
}
count = number of iterations
varName = loop variable (starts at 1)

**Errors**
Unknown or invalid command: <line>
Execution stops immediately when an error occurs.

**Version**
v14025.50 (beta)
