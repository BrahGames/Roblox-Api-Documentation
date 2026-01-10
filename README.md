# Runner Script Syntax

A minimal line-based scripting language executed by the Runner class to control events, messages, items, and timing across experiences.

**Rules**
- Commands are **case-sensitive**
- Strings must use **double quotes**: "like this"
- Script runs **top → bottom**
- Empty lines are ignored
- First invalid/unknown command **stops execution**
- Whitespace at line start/end is trimmed

**Tokens & Types**
- **String**: "Hello world"
- **Number**: 123 (also supports decimals when used in define/value resolution)
- **Identifier (variable name)**: letters/numbers/underscore (e.g. myVar, coins_1)

**Variables**
Syntax: define <name> = <value>
- <name> must be an identifier
- <value> resolves in this order:
  1) "quoted string" → string (quotes removed)
  2) numeric text → number
  3) existing variable name → that variable’s value
  4) otherwise → literal text as a string

Examples:
define amount = 5
define title = "Weekend Event"
define copies = amount

**String Expressions**
Used by: print, message text
Operator: ..
- Splits by ".." and concatenates parts into a string
- Each part can be:
  - "quoted string" → included
  - variable name → included (stringified)
  - unknown token → becomes "" (empty string)

Example:
define name = "Alex"
print "Hello " .. name .. "!"

**Events & Actions Available**
These are the actions your script can trigger (implemented in Runner via eventManager):
- **Global Message**: post a message to all experiences (optionally targeted by userId)
- **Admin Event**: start an admin event by name; end it by name
  - Event names are **free-form strings** in quotes (not a fixed enum in code)
- **Happy Hour**: start/end happy hour with message, color, duration, and optional pricing modifiers
- **Admin Item Spawns**: spawn AdminEgg and/or AdminCrate in the map

Notes:
- **Admin Event names**: any string you pass (e.g. "Double Drops", "Weekend Madness"). The Runner does not validate allowed names; downstream systems may.
- **Happy Hour colors**: any single word token (no spaces). The Runner does not validate allowed colors; downstream systems may.

**Commands**

**print**
Syntax: print <expression>
- Prints the evaluated expression

**wait**
Syntax: wait <seconds>
- <seconds> must be an integer

**version / v**
Syntax: version
Syntax: v
- Prints: v14025.50 (beta)

**item**
Syntax: item <ItemName> [amount?]
- <ItemName> options (case-sensitive): All | Crate | Egg
- amount? optional integer; defaults to 1

Behavior:
- item All [n?] spawns:
  - AdminEgg x n
  - AdminCrate x n
- item Egg [n?] spawns:
  - AdminEgg x n
- item Crate [n?] spawns:
  - AdminCrate x n

**message**
Syntax: message <expression> [userIdToken?]
- <expression> is everything up to the last token (unless there is only one token)
- userIdToken? is optional and must be a single token (no spaces)
- userIdToken resolves using normal value resolution; only used if it resolves to a **number**
- If userIdToken is missing or not numeric, the message is posted without a userId target

Important:
- Because userIdToken is parsed as the **last token**, if you want the message to end with something that looks like an ID, wrap it in quotes as part of the expression.
- The expression itself supports ".." concatenation.

Examples:
message "Server restarting soon"
message "Hello " .. name 123456789
message "User: " .. name .. " joined!"

**admin**
Syntax: admin "<eventName>"
- Starts an admin event in all experiences
- <eventName> is required and must be in double quotes

Example:
admin "Double Drops"

**admin end**
Syntax: admin end "<eventName>"
- Ends the specified admin event in all experiences
- <eventName> is required and must be in double quotes

Example:
admin end "Double Drops"

**happyhour**
Syntax: happyhour "<message>" <color> <durationSeconds> [priceset:<number>?] [pricepercentage:<number>?]
- <message> required, in double quotes
- <color> required, a single word token (no spaces)
- <durationSeconds> required, integer
- priceset:<number>? optional
- pricepercentage:<number>? optional

Notes:
- Both options can be provided, in any order
- Unknown options are ignored (only these two are parsed)

Examples:
happyhour "Happy Hour Live!" Red 300
happyhour "Flash Sale!" Blue 120 pricepercentage:25
happyhour "Fixed Prices!" Green 600 priceset:49
happyhour "Mixed" Purple 900 priceset:99 pricepercentage:15

**happyhour end**
Syntax: happyhour end
- Ends happy hour

**Loops**
Syntax:
loop for <count>; <varName> {
  <commands...>
}
- <count> required integer
- <varName> required identifier
- Block ends when a line is exactly: }
- <varName> is set to 1..count for each iteration

Example:
loop for 3; i {
  print "Run " .. i
  wait 1
}

**Errors**
On the first invalid line:
Unknown or invalid command: <line>
- Includes the script line number in Runner output
- Execution stops immediately

**Version**
v14025.50 (beta)
