# Types

### array

Keyword used to explicitly declare the "array" type of a variable or a parameter. Array objects (or IDs) can be created with the array.new<type>, array.from function.

**EXAMPLE**

```pine
//@version=6
indicator("array", overlay=true)
array<float> a = na
a := array.new<float>(1, close)
plot(array.get(a, 0))
```

**REMARKS**

Array objects are always of "series" form.

**SEE ALSO**

var, line, label, table, box, array.new<type>, array.from

---

### bool

Keyword used to explicitly declare the "bool" (boolean) type of a variable or a parameter. "Bool" variables can have values true or false.

**EXAMPLE**

```pine
//@version=6
indicator("bool")
bool b = true    // Same as `b = true`
plot(b ? open : close)
```

**REMARKS**

Explicitly mentioning the type in a variable declaration is optional. Learn more about Pine Script® types in the User Manual page on the Type System.

**SEE ALSO**

var, varip, int, float, color, string, true, false

---

### box

Keyword used to explicitly declare the "box" type of a variable or a parameter. Box objects (or IDs) can be created with the box.new function.

**EXAMPLE**

```pine
//@version=6
indicator("box")
// Empty `box1` box ID.
var box box1 = na
// `box` type is unnecessary because `box.new()` returns a "box" type.
var box2 = box.new(na, na, na, na)
box3 = box.new(time, open, time + 60 * 60 * 24, close, xloc=xloc.bar_time)
```

**REMARKS**

Box objects are always of "series" form.

**SEE ALSO**

var, line, label, table, box.new

---

### chart.point

Keyword to explicitly declare the type of a variable or parameter as chart.point. Scripts can produce chart.point instances using the chart.point.from_time, chart.point.from_index, chart.point.now, and chart.point.new functions.

**FIELDS**

- **index (series int)** The x-coordinate of the point, expressed as a bar index value.
- **time (series int)** The x-coordinate of the point, expressed as a UNIX time value, in milliseconds.
- **price (series float)** The y-coordinate of the point.

**SEE ALSO**

polyline

---

### color

Keyword used to explicitly declare the "color" type of a variable or a parameter.

**EXAMPLE**

```pine
//@version=6
indicator("color", overlay = true)

color textColor = color.green
color labelColor = #FF000080 // Red color (FF0000) with 50% transparency (80 which is half of FF).
if barstate.islastconfirmedhistory
    label.new(bar_index, high, text = "Label", color = labelColor, textcolor = textColor)

// When declaring variables with color literals, built-in constants(color.green) or functions (color.new(), color.rgb()), the "color" keyword for the type can be omitted.
c = color.rgb(0,255,0,0)
plot(close, color = c)
```

**REMARKS**

Color literals have the following format: #RRGGBB or #RRGGBBAA. The letter pairs represent 00 to FF hexadecimal values (0 to 255 in decimal) where RR, GG and BB pairs are the values for the color's red, green and blue components. AA is an optional value for the color's transparency (or alpha component) where 00 is invisible and FF opaque. When no AA pair is supplied, FF is used. The hexadecimal letters can be upper or lower case.

Explicitly mentioning the type in a variable declaration is optional, except when it is initialized with na. Learn more about Pine Script® types in the User Manual page on the Type System.

**SEE ALSO**

var, varip, int, float, string, color.rgb, color.new

---

### const

The const keyword explicitly assigns the "const" type qualifier to variables and the parameters of non-exported functions. Variables and parameters with the "const" qualifier reference values established at compile time that never change in the script's execution.

In variable declarations, the compiler can usually infer the qualified type automatically based on the values assigned to a variable, and it can automatically change a variable's qualifier to a stronger one when necessary. The type qualifier hierarchy is "const" < "input" < "simple" < "series", where "const" is the weakest.

Explicitly declaring a variable with the const keyword restricts the type qualifier to "const", meaning the variable cannot accept a value with a stronger qualifier (e.g., "input"), nor can the value assigned to the variable change at any point in the script's execution.

When using this keyword to specify the type qualifier, one must also use a type keyword to declare the allowed type.

**SYNTAX**

```
[method ]<functionName>([const <paramType> ]<paramName>[ = <defaultValue>])

[var/varip ]const <variableType> <variableName> = <variableValue>
```

**EXAMPLE**

```pine
//@version=6
indicator("custom plot title")

//@function Concatenates two "const string" values.
concatStrings(const string x, const string y) =>
    const string result = x + y

//@variable The title of the plot.
const string myTitle = concatStrings("My ", "Plot")

plot(close, myTitle)
```

**EXAMPLE**

```pine
//@version=6
indicator("can't assign input to const")

//@variable A variable declared as "const float" that attempts to assign the result of `input.float()` as its value.
//          This declaration causes an error. The "input float" qualified type is stronger than "const float".
const float myVar = input.float(2.0)

plot(myVar)
```

**REMARKS**

To learn more, see our User Manual's section on type qualifiers.

**SEE ALSO**

simple, series

---

### float

Keyword used to explicitly declare the "float" (floating point) type of a variable or a parameter.

**EXAMPLE**

```pine
//@version=6
indicator("float")
float f = 3.14    // Same as `f = 3.14`
f := na
plot(f)
```

**REMARKS**

Explicitly mentioning the type in a variable declaration is optional, except when it is initialized with na. Learn more about Pine Script® types in the User Manual page on the Type System.

**SEE ALSO**

var, varip, int, bool, color, string

---

### int

Keyword used to explicitly declare the "int" (integer) type of a variable or a parameter.

**EXAMPLE**

```pine
//@version=6
indicator("int")
int i = 14    // Same as `i = 14`
i := na
plot(i)
```

**REMARKS**

Explicitly mentioning the type in a variable declaration is optional, except when it is initialized with na. Learn more about Pine Script® types in the User Manual page on the Type System.

**SEE ALSO**

var, varip, float, bool, color, string

---

### label

Keyword used to explicitly declare the "label" type of a variable or a parameter. Label objects (or IDs) can be created with the label.new function.

**EXAMPLE**

```pine
//@version=6
indicator("label")
// Empty `label1` label ID.
var label label1 = na
// `label` type is unnecessary because `label.new()` returns "label" type.
var label2 = label.new(na, na, na)
if barstate.islastconfirmedhistory
    label3 = label.new(bar_index, high, text = "label3 text")
```

**REMARKS**

Label objects are always of "series" form.

**SEE ALSO**

var, line, box, label.new

---

### line

Keyword used to explicitly declare the "line" type of a variable or a parameter. Line objects (or IDs) can be created with the line.new function.

**EXAMPLE**

```pine
//@version=6
indicator("line")
// Empty `line1` line ID.
var line line1 = na
// `line` type is unnecessary because `line.new()` returns "line" type.
var line2 = line.new(na, na, na, na)
line3 = line.new(bar_index - 1, high, bar_index, high, extend = extend.right)
```

**REMARKS**

Line objects are always of "series" form.

**SEE ALSO**

var, label, box, line.new

---

### linefill

Keyword used to explicitly declare the "linefill" type of a variable or a parameter. Linefill objects (or IDs) can be created with the linefill.new function.

**EXAMPLE**

```pine
//@version=6
indicator("linefill", overlay=true)
// Empty `linefill1` line ID.
var linefill linefill1 = na
// `linefill` type is unnecessary because `linefill.new()` returns "linefill" type.
var linefill2 = linefill.new(na, na, na)

if barstate.islastconfirmedhistory
    line1 = line.new(bar_index - 10, high+1, bar_index, high+1, extend = extend.right)
    line2 = line.new(bar_index - 10, low+1, bar_index, low+1, extend = extend.right)
    linefill3 = linefill.new(line1, line2, color = color.new(color.green, 80))
```

**REMARKS**

Linefill objects are always of "series" form.

**SEE ALSO**

var, line, label, table, box, linefill.new

---

### map

Keyword used to explicitly declare the "map" type of a variable or a parameter. Map objects (or IDs) can be created with the map.new<type,type> function.

**EXAMPLE**

```pine
//@version=6
indicator("map", overlay=true)
map<int, float> a = na
a := map.new<int, float>()
a.put(bar_index, close)
label.new(bar_index, a.get(bar_index), "Current close")
```

**REMARKS**

Map objects are always of series form.

**SEE ALSO**

map.new<type,type>

---

### matrix

Keyword used to explicitly declare the "matrix" type of a variable or a parameter. Matrix objects (or IDs) can be created with the matrix.new<type> function.

**EXAMPLE**

```pine
//@version=6
indicator("matrix example")

// Create `m1` matrix of `int` type.
matrix<int> m1 = matrix.new<int>(2, 3, 0)

// `matrix<int>` is unnecessary because the `matrix.new<int>()` function returns an `int` type matrix object.
m2 = matrix.new<int>(2, 3, 0)

// Display matrix using a label.
if barstate.islastconfirmedhistory
    label.new(bar_index, high, str.tostring(m2))
```

**REMARKS**

Matrix objects are always of "series" form.

**SEE ALSO**

var, matrix.new<type>, array

---

### polyline

Keyword to explicitly declare the type of a variable or parameter as polyline. Scripts can produce polyline instances using the polyline.new function.

**SEE ALSO**

chart.point

---

### series

The series keyword explicitly assigns the "series" type qualifier to variables and function parameters. Variables and parameters that use the "series" qualifier can reference values that change throughout a script's execution.

Explicit use of the series keyword when declaring the parameters of a library's exported functions is typically unnecessary, as the compiler can usually automatically detect whether a parameter is compatible with "series" or "simple" qualified values. By default, all exported function parameters are qualified as "series" wherever possible.

In variable declarations, the compiler can usually infer the qualified type automatically based on the values assigned to a variable, and it can automatically change a variable's qualifier to a stronger one when necessary. The type qualifier hierarchy is "const" < "input" < "simple" < "series", where "series" is the strongest.

Explicitly declaring a variable with the series keyword restricts the type qualifier to "series", meaning the script cannot pass its value to any variable or function parameter that requires a value with a weaker qualifier ("const", "input", or "simple").

When using this keyword to specify the type qualifier, one must also use a type keyword to declare the allowed type.

**SYNTAX**

```
export [method ]<functionName>([[series ]<paramType>] <paramName>[ = <defaultValue>])

[method ]<functionName>([series <paramType> ]<paramName>[ = <defaultValue>])

[var/varip ]series <variableType> <variableName> = <variableValue>
```

**EXAMPLE**

```pine
//@version=6
//@description A library with custom functions.
library("CustomFunctions", overlay = true)

//@function Finds the highest `source` value over `length` bars, filtered by the `cond` condition.
export conditionalHighest(series float source, series bool cond, series int length) =>
    //@variable The highest `source` value from when the `cond` was `true` over `length` bars.
    series float result = na
    // Loop to find the highest value.
    for i = 0 to length - 1
        if cond[i]
            value   = source[i]
            result := math.max(nz(result, value), value)
    // Return the `result`.
    result

//@variable Is `true` once every five bars.
series bool condition = bar_index % 5 == 0

//@variable The highest `close` value from every fifth bar over the last 100 bars.
series float hiValue = conditionalHighest(close, condition, 100)

plot(hiValue)
bgcolor(condition ? color.new(color.teal, 80) : na)
```

**EXAMPLE**

```pine
//@version=6
indicator("series variable not allowed")

//@variable A variable declared as "series int" with a value of 5.
series int myVar = 5

// This call causes an error.
// The `histbase` accepts "input int/float". It can't accept the stronger "series int" qualified type.
plot(close, style = plot.style_histogram, histbase = myVar)
```

**REMARKS**

To learn more, see our User Manual's section on type qualifiers.

**SEE ALSO**

simple, const

---

### simple

The simple keyword explicitly assigns the "simple" type qualifier to variables and function parameters. Variables and parameters that use the "simple" qualifier can reference values established at the beginning of a script's execution that do not change later.

To restrict the parameters in a library's exported functions to only allow values with a "simple" or weaker type qualifier, using the simple keyword when declaring parameters is often necessary, as libraries automatically qualify all parameters as "series" wherever possible by default. Explicitly restricting functions to accept "simple" arguments also allows them to return "simple" values in some cases, depending on the operations they execute, making them usable with the parameters of built-in functions that do not allow "series" arguments.

In variable declarations, the compiler can usually infer the qualified type automatically based on the values assigned to a variable, and it can automatically change a variable's qualifier to a stronger one when necessary. The type qualifier hierarchy is "const" < "input" < "simple" < "series", where "simple" is stronger than "input" and "const".

Explicitly declaring a variable with the simple keyword restricts the type qualifier to "simple", meaning the script cannot pass its value to any variable or function parameter that requires a value with a weaker qualifier ("const" or "input"). Additionally, one cannot assign a "series" value to a variable explicitly declared with the simple keyword.

When using this keyword to specify the type qualifier, one must also use a type keyword to declare the allowed type.

**SYNTAX**

```
export [method ]<functionName>([[simple ]<paramType>] <paramName>[ = <defaultValue>])

[method ]<functionName>([simple <paramType> ]<paramName>[ = <defaultValue>])

[var/varip ]simple <variableType> <variableName> = <variableValue></variableValue>
```

**EXAMPLE**

```pine
//@version=6
//@description A library with custom functions.
library("CustomFunctions", overlay = true)

//@function         Calculates the length values for a ribbon of four EMAs by multiplying the `baseLength`.
//@param baseLength The initial EMA length. Requires "simple int" because you can't use "series int" in `ta.ema()`.
//@returns          A tuple of length values.
export ribbonLengths(simple int baseLength) =>
    simple int length1 = baseLength
    simple int length2 = baseLength * 2
    simple int length3 = baseLength * 3
    simple int length4 = baseLength * 4
    [length1, length2, length3, length4]

// Get a tuple of "simple int" length values.
[len1, len2, len3, len4] = ribbonLengths(14)

// Plot four EMAs using the values from the tuple.
plot(ta.ema(close, len1), "EMA 1", color = color.red)
plot(ta.ema(close, len2), "EMA 1", color = color.orange)
plot(ta.ema(close, len3), "EMA 1", color = color.green)
plot(ta.ema(close, len4), "EMA 1", color = color.blue)
```

**EXAMPLE**

```pine
//@version=6
indicator("can't change simple to series")

//@variable A variable declared as "simple float" with a value of 5.0.
simple float myVar = 5.0

// This reassignment causes an error.
// The `close` variable returns a "series float" value. Since `myVar` is restricted to "simple" values, it cannot
// change its qualifier to "series".
myVar := close

plot(myVar)
```

**REMARKS**

To learn more, see our User Manual's section on type qualifiers.

**SEE ALSO**

series, const

---

### string

Keyword used to explicitly declare the "string" type of a variable or a parameter.

**EXAMPLE**

```pine
//@version=6
indicator("string")
string s = "Hello World!"    // Same as `s = "Hello world!"`
// string s = na // same as ""
plot(na, title=s)
```

**REMARKS**

Explicitly mentioning the type in a variable declaration is optional, except when it is initialized with na. Learn more about Pine Script® types in the User Manual page on the Type System.

**SEE ALSO**

var, varip, int, float, bool, str.tostring, str.format

---

### table

Keyword used to explicitly declare the "table" type of a variable or a parameter. Table objects (or IDs) can be created with the table.new function.

**EXAMPLE**

```pine
//@version=6
indicator("table")
// Empty `table1` table ID.
var table table1 = na
// `table` type is unnecessary because `table.new()` returns "table" type.
var table2 = table.new(position.top_left, na, na)

if barstate.islastconfirmedhistory
    var table3 = table.new(position = position.top_right, columns = 1, rows = 1, bgcolor = color.yellow, border_width = 1)
    table.cell(table_id = table3, column = 0, row = 0, text = "table3 text")
```

**REMARKS**

Table objects are always of "series" form.

**SEE ALSO**

var, line, label, box, table.new
