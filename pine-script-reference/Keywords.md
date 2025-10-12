# Keywords

### and

Logical AND. Applicable to boolean expressions.

**SYNTAX**

```
expr1 and expr2
```

**RETURNS**

Boolean value, or series of boolean values.

**REMARKS**

If expr1 evaluates to false, the and operator returns false without evaluating expr2.

---

### enum

This keyword allows the creation of an enumeration, enum for short. Enums are unique constructs that hold groups of predefined constants.

Each field in an enum has a const string title. Scripts can access the fields in an enum using dot notation, similar to accessing the fields of a user-defined type.

Each field represents a value of the enumName enum. Scripts can declare each field in an enum with an optional const string title. If a field's title is not specified, its title is the string representation of its name. Use str.tostring on an enum field to retrieve its title.

**SYNTAX**

```
[export ]enum <enumName>
<field_1> [= <title_1>]
<field_2> [= <title_2>]
...
<field_N> [= <title_N>]
```

One can use an enum to quickly create a dropdown input with the help of the input.enum function. The options that appear in the dropdown represent the titles of the enum fields.

**EXAMPLE**

```pine
//@version=6
indicator("Session highlight", overlay = true)

//@enum       Contains fields with popular timezones as titles.
//@field exch Has an empty string as the title to represent the chart timezone.
enum tz
    utc  = "UTC"
    exch = ""
    ny   = "America/New_York"
    chi  = "America/Chicago"
    lon  = "Europe/London"
    tok  = "Asia/Tokyo"

//@variable The session string.
selectedSession = input.session("1200-1500", "Session")
//@variable The selected timezone. The input's dropdown contains the fields in the `tz` enum.
selectedTimezone = input.enum(tz.utc, "Session Timezone")

//@variable Is `true` if the current bar's time is in the specified session.
bool inSession = false
if not na(time("", selectedSession, str.tostring(selectedTimezone)))
    inSession := true

// Highlight the background when `inSession` is `true`.
bgcolor(inSession ? color.new(color.green, 90) : na, title = "Active session highlight")
```

Additionally, one can use an enum in a collection's type template to restrict the values it will allow as elements. When used inside a type template, the collection will only accept fields that belong to the specified enum.

**EXAMPLE**

```pine
//@version=6
indicator("Map with enum keys")

//@enum        Contains fields with titles representing ticker IDs.
//@field aapl  Has an Apple ticker ID as its title.
//@field tsla  Has a Tesla ticker ID as its title.
//@field amzn  Has an Amazon ticker ID as its title.
enum symbols
    aapl = "NASDAQ:AAPL"
    tsla = "NASDAQ:TSLA"
    amzn = "NASDAQ:AMZN"

//@variable A map that accepts fields from the `symbols` enum as keys and "float" values.
map<symbols, float> data = map.new<symbols, float>()
// Put key-value pairs into the `data` map.
data.put(symbols.aapl, request.security(str.tostring(symbols.aapl), timeframe.period, close))
data.put(symbols.tsla, request.security(str.tostring(symbols.tsla), timeframe.period, close))
data.put(symbols.amzn, request.security(str.tostring(symbols.amzn), timeframe.period, close))
// Plot the value from the `data` map accessed by the `symbols.aapl` key.
plot(data.get(symbols.aapl))
```

---

### export

Used in libraries to prefix the declaration of functions or user-defined type definitions that will be available from other scripts importing the library.

**EXAMPLE**

```pine
//@version=6
//@description Library of debugging functions.
library("Debugging_library", overlay = true)
//@function Displays a string as a table cell for debugging purposes.
//@param txt String to display.
//@returns Void.
export print(string txt) =>
    var table t = table.new(position.middle_right, 1, 1)
    table.cell(t, 0, 0, txt, bgcolor = color.yellow)
// Using the function from inside the library to show an example on the published chart.
// This has no impact on scripts using the library.
print("Library Test")
```

**REMARKS**

Each library must have at least one exported function or user-defined type (UDT).

Exported functions cannot use variables from the global scope if they are arrays, mutable variables (reassigned with :=), or variables of 'input' form.

Exported functions cannot use request.*() functions.

Exported functions must explicitly declare each parameter's type and all parameters must be used in the function's body. By default, all arguments passed to exported functions are of the series form, unless they are explicitly specified as simple in the function's signature.

The @description, @function, @param, @type, @field, and @returns compiler annotations are used to automatically generate the library's description and release notes, and in the Pine Script® Editor's tooltips.

**SEE ALSO**

library, import, simple, series, type

---

### for

Creates a count-controlled loop, which uses a counter variable to manage the iterative executions of its local code block. The loop continues new iterations until the counter reaches a specified final value.

**SYNTAX**

```
[variables =|:=] for counter = from_num to to_num [by step_num]
    statements | continue | break
    return_expression
```

variables (return_expression type) Optional. A declared variable or tuple to hold the values or references from the last evaluation of the return_expression after the loop terminates. The script can assign the loop's returned results to variables only if the results are not "void". If the loop's conditions prevent iteration, or if no iterations evaluate the return_expression, the variables' assigned values and references are na.

counter (series int/float) The counter variable. The loop increments the variable's value from the initial value (from_num) to the final value (to_num) by a fixed amount (step_num) after each iteration. The last possible iteration occurs when the variable's value reaches the to_num value.

from_num (series int/float) The value of the counter variable on the loop's first iteration.

to_num (series int/float) The final counter value for which the loop's header allows a new iteration. The loop increments the counter value by the step_num until it reaches or passes this value. If the script modifies this value during a loop iteration, the loop header uses the new value to control the allowed subsequent iterations.

step_num (series int/float) Optional. A positive value specifying the amount by which the counter value increases or decreases until it reaches or passes the to_num value. If the from_num value is greater than the initial to_num value, the loop subtracts this amount from the counter value after each iteration. Otherwise, the loop adds this amount after each iteration. The default is 1.

statements The code statements and expressions within the loop's body, i.e., the indented block of code beneath the loop header.

return_expression (any type) The last code line or block within the loop's body. The loop returns the results from this code after the final iteration. If the loop stops prematurely due to a continue or break statement, the returned values or references are those of the latest iteration that evaluated this code. To use the loop's returned results, assign them to a variable or tuple.

continue A loop-specific keyword that instructs the script to skip the remainder of the current loop iteration and continue to the next iteration.

break A loop-specific keyword that prompts the script to stop the current iteration and exit the loop entirely.

**EXAMPLE**

```pine
//@version=6
indicator("Basic `for` loop")

//@function Calculates the number of bars in the last `length` bars that have their `close` above the current `close`.
//@param length The number of bars used in the calculation.
greaterCloseCount(length) =>
    int result = 0
    for i = 1 to length
        if close[i] > close
            result += 1
    result

plot(greaterCloseCount(14))
```

**EXAMPLE**

```pine
//@version=6
indicator("`for` loop with a step")

a = array.from(0, 1, 2, 3, 4, 5, 6, 7, 8, 9)
sum = 0.0

for i = 0 to 9 by 5
    // Because the step is set to 5, we are adding only the first (0) and the sixth (5) value from the array `a`.
    sum += array.get(a, i)

plot(sum)
```

**REMARKS**

Modifying a loop's to_num value during an iteration does not change the direction of the loop's counter. For a loop that counts upward, setting the to_num to a value less than the from_num value on an iteration stops the loop immediately after that iteration ends. Likewise, a loop that counts downward stops after an iteration where the to_num value becomes greater than the from_num value.

**SEE ALSO**

for...in, while

---

### for...in

The for...in structure allows the repeated execution of a number of statements for each element in an array. It can be used with either one argument: array_element, or with two: [index, array_element]. The second form doesn't affect the functionality of the loop. It tracks the current iteration's index in the tuple's first variable.

**SYNTAX**

```
[var_declaration =] for array_element in array_id
    statements | continue | break
    return_expression

[var_declaration =] for [index, array_element] in array_id
    statements | continue | break
    return_expression
```

var_declaration - An optional variable declaration that will be assigned the value of the loop's return_expression.

index - An optional variable that tracks the current iteration's index. Indexing starts at 0. The variable is immutable in the loop's body. When used, it must be included in a tuple also containing array_element.

array_element - A variable containing each successive array element to be processed in the loop. The variable is immutable in the loop's body.

array_id - The ID of the array over which the loop is iterated.

statements | continue | break - Any number of statements, or the 'continue' or 'break' keywords, indented by 4 spaces or a tab.

return_expression - The loop's return value assigned to the variable in var_declaration, if one is present. If the loop exits because of a 'continue' or 'break' keyword, the loop's return value is that of the last variable assigned a value before the loop's exit.

continue - A keyword that can only be used in loops. It causes the next iteration of the loop to be executed.

break - A keyword that exits the loop.

Scripts can modify arrays and matrices while iterating over their elements with this structure. However, maps cannot change while looping through their key-value pairs. To modify a map within a for...in loop, iterate over the key-value pairs of a copy or over the elements in its map.keys array.

Here, we use the single-argument form of for...in to determine on each bar how many of the bar's OHLC values are greater than the SMA of 'close' values:

**EXAMPLE**

```pine
//@version=6
indicator("for...in")
// Here we determine on each bar how many of the bar's OHLC values are greater than the SMA of 'close' values
array<float> ohlcValues = array.from(open, high, low, close)
qtyGreaterThan(value, array) =>
    int result = 0
    for currentElement in array
        if currentElement > value
            result += 1
        result
plot(qtyGreaterThan(ta.sma(close, 20), ohlcValues))
```

Here, we use the two-argument form of for...in to set the values of our isPos array to true when their corresponding value in our valuesArray array is positive:

**EXAMPLE**

```pine
//@version=6
indicator("for...in")
var valuesArray = array.from(4, -8, 11, 78, -16, 34, 7, 99, 0, 55)
var isPos = array.new_bool(10, false)

for [index, value] in valuesArray
    if value > 0
        array.set(isPos, index, true)

if barstate.islastconfirmedhistory
    label.new(bar_index, high, str.tostring(isPos))
```

Iterate through matrix rows as arrays.

**EXAMPLE**

```pine
//@version=6
indicator("`for ... in` matrix Example")

// Create a 2x3 matrix with values `4`.
matrix1 = matrix.new<int>(2, 3, 4)

sum = 0.0
// Loop through every row of the matrix.
for rowArray in matrix1
    // Sum values of the every row
    sum += array.sum(rowArray)

plot(sum)
```

**SEE ALSO**

for, while, array.sum, array.min, array.max

---

### if

If statement defines what block of statements must be executed when conditions of the expression are satisfied.

To have access to and use the if statement, one should specify the version >= 2 of Pine Script® language in the very first line of code, for example: //@version=6

The 4th version of Pine Script® Language allows you to use “else if” syntax.

General code form:

**SYNTAX**

```
var_declarationX = if condition
    var_decl_then0
    var_decl_then1
    …
    var_decl_thenN
else if [optional block]
    var_decl_else0
    var_decl_else1
    …
    var_decl_elseN
else
    var_decl_else0
    var_decl_else1
    …
    var_decl_elseN
    return_expression_else
```

where

var_declarationX — this variable gets the value of the if statement

condition — if the condition is true, the logic from the block 'then' (var_decl_then0, var_decl_then1, etc.) is used.

If the condition is false, the logic from the block 'else' (var_decl_else0, var_decl_else1, etc.) is used.

return_expression_then, return_expression_else — the last expression from the block then or from the block else will return the final value of the statement. If declaration of the variable is in the end, its value will be the result.

The type of returning value of the if statement depends on return_expression_then and return_expression_else type (their types must match: it is not possible to return an integer value from then, while you have a string value in else block).

**EXAMPLE**

```pine
//@version=6
indicator("if")
// This code compiles
x = if close > open
    close
else
    open

// This code doesn’t compile
// y = if close > open
//     close
// else
//     "open"
plot(x)
```

It is possible to omit the else block. In this case if the condition is false, an “empty” value (na, false, or “”) will be assigned to the var_declarationX variable:

**EXAMPLE**

```pine
//@version=6
indicator("if")
x = if close > open
    close
// If current close > current open, then x = close.
// Otherwise the x = na.
plot(x)
```

It is possible to use either multiple “else if” blocks or none at all. The blocks “then”, “else if”, “else” are shifted by four spaces:

**EXAMPLE**

```pine
//@version=6
indicator("if")
x = if open > close
    5
else if high > low
    close
else
    open
plot(x)
```

It is possible to ignore the resulting value of an if statement (“var_declarationX=“ can be omitted). It may be useful if you need the side effect of the expression, for example in strategy trading:

**EXAMPLE**

```pine
//@version=6
strategy("if")
if (ta.crossover(high, low))
    strategy.entry("BBandLE", strategy.long, stop=low, oca_name="BollingerBands", oca_type=strategy.oca.cancel, comment="BBandLE")
else
    strategy.cancel(id="BBandLE")
```

If statements can include each other:

**EXAMPLE**

```pine
//@version=6
indicator("if")
float x = na
if close > open
    if close > close[1]
        x := close
    else
        x := close[1]
else
    x := open
plot(x)
```

---

### import

Used to load an external library into a script and bind its functions to a namespace. The importing script can be an indicator, a strategy, or another library. A library must be published (privately or publicly) before it can be imported.

**SYNTAX**

```
import {username}/{libraryName}/{libraryVersion} as {alias}
```

**ARGUMENTS**

- **username (literal string)** User name of the library's author.
- **libraryName (literal string)** Name of the imported library, which corresponds to the title argument used by the author in his library script.
- **libraryVersion (literal int)** Version number of the imported library.
- **alias (literal string)** A non-numeric identifier used as a namespace to refer to the library's functions. Optional. The default is the libraryName string.

**EXAMPLE**

```pine
//@version=6
indicator("num_methods import")
// Import the first version of the username’s "num_methods" library and assign it to the "m" namespace",
import username/num_methods/1 as m
// Call the “sinh()” function from the imported library
y = m.sinh(3.14)
// Plot value returned by the "sinh()" function",
plot(y)
```

**REMARKS**

Using an alias that replaces a built-in namespace such as math.* or strategy.* is allowed, but if the library contains function names that shadow Pine Script®'s built-in functions, the built-ins will become unavailable. The same version of a library can only be imported once. Aliases must be distinct for each imported library. When calling library functions, casting their arguments to types other than their declared type is not allowed. An import statement cannot use 'as' or 'import' as username, libraryName, or alias identifiers.

**SEE ALSO**

library, export

---

### method

This keyword is used to prefix a function declaration, indicating it can then be invoked using dot notation by appending its name to a variable of the type of its first parameter and omitting that first parameter. Alternatively, functions declared as methods can also be invoked like normal user-defined functions. In that case, an argument must be supplied for its first parameter.

The first parameter of a method declaration must be explicitly typified.

**SYNTAX**

```
[export] method <functionName>(<paramType> <paramName> [= <defaultValue>], …) =>
    <functionBlock>
```

**EXAMPLE**

```pine
//@version=6
indicator("")

var prices = array.new<float>()

//@function Pushes a new value into the array and removes the first one if the resulting array is greater than `maxSize`. Can be used as a method.
method maintainArray(array<float> id, maxSize, value) =>
    id.push(value)
    if id.size() > maxSize
        id.shift()

prices.maintainArray(50, close)
// The method can also be called like a function, without using dot notation.
// In this case an argument must be supplied for its first parameter.
// maintainArray(prices, 50, close)

// This calls the `array.avg()` built-in using dot notation with the `prices` array.
// It is possible because built-in functions belonging to some namespaces that are a special Pine type
// can be invoked with method notation when the function's first parameter is an ID of that type.
// Those namespaces are: `array`, `matrix`, `line`, `linefill`, `label`, `box`, and `table`.
plot(prices.avg())
```

---

### not

Logical negation (NOT). Applicable to boolean expressions.

**SYNTAX**

```
not expr1
```

**RETURNS**

Boolean value, or series of boolean values.

---

### or

Logical OR. Applicable to boolean expressions.

**SYNTAX**

```
expr1 or expr2
```

**RETURNS**

Boolean value, or series of boolean values.

**REMARKS**

If expr1 evaluates to true, the or operator returns true without evaluating expr2.

---

### switch

The switch operator transfers control to one of the several statements, depending on the values of a condition and expressions.

**SYNTAX**

```
[variable_declaration = ] switch expression
    value1 => local_block
    value2 => local_block
    …
    => default_local_block

[variable_declaration = ] switch
    condition1 => local_block
    condition2 => local_block
    …
    => default_local_block
```

Switch with an expression:

**EXAMPLE**

```pine
//@version=6
indicator("Switch using an expression")

string i_maType = input.string("EMA", "MA type", options = ["EMA", "SMA", "RMA", "WMA"])

float ma = switch i_maType
    "EMA" => ta.ema(close, 10)
    "SMA" => ta.sma(close, 10)
    "RMA" => ta.rma(close, 10)
    // Default used when the three first cases do not match.
    => ta.wma(close, 10)

plot(ma)
```

Switch without an expression:

**EXAMPLE**

```pine
//@version=6
strategy("Switch without an expression", overlay = true)

bool longCondition  = ta.crossover( ta.sma(close, 14), ta.sma(close, 28))
bool shortCondition = ta.crossunder(ta.sma(close, 14), ta.sma(close, 28))

switch
    longCondition  => strategy.entry("Long ID", strategy.long)
    shortCondition => strategy.entry("Short ID", strategy.short)
```

**RETURNS**

The value of the last expression in the local block of statements that is executed.

**REMARKS**

Only one of the local_block instances or the default_local_block can be executed. The default_local_block is introduced with the => token alone and is only executed when none of the preceding blocks are executed. If the result of the switch statement is assigned to a variable and a default_local_block is not specified, the statement returns na if no local_block is executed. When assigning the result of the switch statement to a variable, all local_block instances must return the same type of value.

**SEE ALSO**

if, ?:

---

### type

This keyword allows the declaration of user-defined types (UDT) from which scripts can instantiate objects. UDTs are composite types that contain an arbitrary number of fields of any built-in or user-defined type, including the defined UDT itself. The syntax to define a UDT is:

**SYNTAX**

```
[export ]type <UDT_identifier>
    [varip ]<field_type> <field_name> [= <value>]
    …
```

Once a UDT is defined, scripts can instantiate objects from it with the UDT_identifier.new() construct. When creating a new type instance, the fields of the resulting object will initialize with the default values from the UDT's definition. Any type fields without specified defaults will initialize as na. Alternatively, users can pass initial values as arguments in the *.new() method to override the type's defaults. For example, newFooObject = foo.new(x = true) assigns a new foo object to the newFooObject variable with its x field initialized using a value of true.

Field declarations can include the varip keyword, in which case the field values persist between successive script iterations on the same bar.

For more information see the User Manual's sections on defining UDTs and using objects.

Libraries can export UDTs. See the Libraries page of our User Manual to learn more.

**EXAMPLE**

```pine
//@version=6
indicator("Multi Time Period Chart", overlay = true)

timeframeInput = input.timeframe("1D")

type bar
    float o = open
    float h = high
    float l = low
    float c = close
    int   t = time

drawBox(bar b, right) =>
    color boxColor = b.c >= b.o ? color.green : color.red
    box.new(b.t, b.h, right, b.l, boxColor, xloc = xloc.bar_time, bgcolor = color.new(boxColor, 90))

updateBox(box boxId, bar b) =>
    color boxColor = b.c >= b.o ? color.green : color.red
    box.set_border_color(boxId, boxColor)
    box.set_bgcolor(boxId, color.new(boxColor, 90))
    box.set_top(boxId, b.h)
    box.set_bottom(boxId, b.l)
    box.set_right(boxId, time)

secBar = request.security(syminfo.tickerid, timeframeInput, bar.new())

if not na(secBar)
    // To avoid a runtime error, only process data when an object exists.
    if not barstate.islast
        if timeframe.change(timeframeInput)
            // On historical bars, draw a new box in the past when the HTF closes.
            drawBox(secBar, time[1])
    else
        var box lastBox = na
        if na(lastBox) or timeframe.change(timeframeInput)
            // On the last bar, only draw a new current box the first time we get there or when HTF changes.
            lastBox := drawBox(secBar, time)
        else
            // On other chart updates, use setters to modify the current box.
            updateBox(lastBox, secBar)
```

---

### var

var is the keyword used for assigning and one-time initializing of the variable.

Normally, a syntax of assignment of variables, which doesn’t include the keyword var, results in the value of the variable being overwritten with every update of the data. Contrary to that, when assigning variables with the keyword var, they can “keep the state” despite the data updating, only changing it when conditions within if-expressions are met.

**SYNTAX**

```
var variable_name = expression
```

where:

variable_name - any name of the user’s variable that’s allowed in Pine Script® (can contain capital and lowercase Latin characters, numbers, and underscores (_), but can’t start with a number).

expression - any arithmetic expression, just as with defining a regular variable. The expression will be calculated and assigned to a variable once.

**EXAMPLE**

```pine
//@version=6
indicator("Var keyword example")
var a = close
var b = 0.0
var c = 0.0
var green_bars_count = 0
if close > open
    var x = close
    b := x
    green_bars_count := green_bars_count + 1
    if green_bars_count >= 10
        var y = close
        c := y
plot(a)
plot(b)
plot(c)
```

The variable 'a' keeps the closing price of the first bar for each bar in the series.

The variable 'b' keeps the closing price of the first "green" bar in the series.

The variable 'c' keeps the closing price of the tenth "green" bar in the series.

---

### varip

varip (var intrabar persist) is the keyword used for the assignment and one-time initialization of a variable or a field of a user-defined type. It’s similar to the var keyword, but variables and fields declared with varip retain their values between executions of the script on the same bar.

**SYNTAX**

```
varip [<variable_type> ]<variable_name> = <expression>

[export ]type <UDT_identifier>
    varip <field_type> <field_name> [= <value>]
```

where:

variable_type - An optional fundamental type (int, float, bool, color, string) or a user-defined type, or an array or matrix of one of those types. Special types are not compatible with this keyword.

variable_name - A valid identifier. The variable can also be an object created from a UDT.

expression - Any arithmetic expression, just as when defining a regular variable. The expression will be calculated and assigned to the variable only once, on the first bar.

UDT_identifier, field_type, field_name, value - Constructs related to user-defined types as described in the type section.

**EXAMPLE**

```pine
//@version=6
indicator("varip")
varip int v = -1
v := v + 1
plot(v)
```

With var, v would equal the value of the bar_index. On historical bars, where the script calculates only once per chart bar, the value of v is the same as with var. However, on realtime bars, the script will evaluate the expression on each new chart update, producing a different result.

**EXAMPLE**

```pine
//@version=6
indicator("varip with types")
type barData
    int index = -1
    varip int ticks = -1

var currBar = barData.new()
currBar.index += 1
currBar.ticks += 1

// Will be equal to bar_index on all bars
plot(currBar.index)
// In real time, will increment per every tick on the chart
plot(currBar.ticks)
```

The same += operation applied to both the index and ticks fields results in different real-time values because ticks increases on every chart update, while index only does so once per bar. Note how the currBar object does not use the varip keyword. The ticks field of the object can increment on every tick, but the reference itself is defined once and then stays unchanged. If we were to declare currBar using varip, the behavior of index would remain unchanged because while the reference to the type instance would persist between chart updates, the index field of the object would not.

**REMARKS**

When using varip to declare variables in strategies that may execute more than once per historical chart bar, the values of such variables are preserved across successive iterations of the script on the same bar.

The effect of varip eliminates the rollback of variables before each successive execution of a script on the same bar.

---

### while

The while statement allows the conditional iteration of a local code block.

**SYNTAX**

```
variable_declaration = while condition
    …
    continue
    …
    break
    …
    return_expression
```

where:

variable_declaration - An optional variable declaration. The return expression can provide the initialization value for this variable.

condition - when true, the local block of the while statement is executed. When false, execution of the script resumes after the while statement.

continue - The continue keyword causes the loop to branch to its next iteration.

break - The break keyword causes the loop to terminate. The script's execution resumes after the while statement.

return_expression - An optional line providing the while statement's returning value.

**EXAMPLE**

```pine
//@version=6
indicator("while")
// This is a simple example of calculating a factorial using a while loop.
int i_n = input.int(10, "Factorial Size", minval=0)
int counter   = i_n
int factorial = 1
while counter > 0
    factorial := factorial * counter
    counter   := counter - 1

plot(factorial)
```

**REMARKS**

The local code block after the initial while line must be indented with four spaces or a tab. For the while loop to terminate, the boolean expression following while must eventually become false, or a break must be executed.
