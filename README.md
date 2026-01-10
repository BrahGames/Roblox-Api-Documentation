# Syntax

## Variables
If you want to use variables then you can do so by using `define`, this keyword creates a global variable.

Example:
```
define variableName = variableType
define age = 30
```

Using the variables, you can use these variables in in-built keywords which support that variable type.

Example:
```
define new = "World"
print "Hello" .. new
```
This will print "Hello World" in output.

## Posting Global Message
In order to put a global message you do so by using `message`

`<> : Required`
`[] : Optional`

Syntax:
```
message <string> [userid]
```

You can combine this with variables

Example:
```
define help = "like"
message "I " .. help
message "I " .. help .. " you!"
```

## Spawning admin items
You can spawn items like `AdminEgg` or `AdminCrate` using `item` command.

`<> : Required`
`[] : Optional`

ItemTypes: `All | Egg | Crate`

Syntax:
```
item <ItemType> [amount]
```

Example:
```
print "This will drop 5 admin eggs and 5 admin crates"
item All 5

print "This will drop 5 admin eggs"
item Egg 5

print "This will drop 5 admin crate"
item Crate 5
```

## Doing admin event
If you want to host event like blizzard, alien etc then you can do so by using `admin`.

`<> : Required`
`[] : Optional`

EventTypes: `Alien | Blizzard | Lightning | Rainbow`
Syntax:
```
admin <EventType[string]>
```

Example:
```
admin "Alien"
```

If you want to end the event then you can do so by 
```
admin end "Alien"
```

## Yielding
Well, compiler do yield between eachline but it depends on request time which cant be set, but if you want a custom yield then u can do so by using `wait`

`<> : Required`
`[] : Optional`


Syntax
```
wait <number>
```

Example:
```
print "hi"
wait 2
print "Bye!"
```

## HappyHour
If you want to host happy hour then u can do so by using `happyhour`

`<> : Required`
`[] : Optional`

Colors: `Green | Gold | Rainbow | Blue | Purple`

Syntax
```
happyhour <"Message"> [durationInSeconds] [Color] [priceset:amount] [pricepercentage:percentageAmount]
```

Example:
```
happyhour "99% SALE!" Green 3600
happyhour "99% SALE!" Green 3600 pricepercentage:99
happyhour "EVERYTHING 5 ROBUX ONLY!" Green 3600 priceset:5
```

Ending happyhour is easy as well.
```
happyhour end
```
and thats it!

## Loops
Everything will be easy when you use loops!! use it by using `loop`

basic english, `loop for` which will create a for loop

Syntax
```
loop for count; variable {
    .. code..
}
```
count is the number, example putting 10 will run loop 10 times and variable stores the current index of the loop.

Example:
```
loop for 5; index {
    print "Current: " .. index
    wait 1
}
```
prints from 1 to 5 every 1 second
`Current 1`
`Current 2`
etc..
