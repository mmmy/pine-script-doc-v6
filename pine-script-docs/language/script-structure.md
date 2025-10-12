# Language / Script structure

> Source: https://www.tradingview.com/pine-script-docs/language/script-structure/
> Retrieved at: 2025-10-12T09:04:09.439Z

# Script structure

A Pine script follows this general structure:

```
<version><declaration_statement><code>
```

## Version

A [compiler annotation](https://www.tradingview.com/pine-script-docs/language/script-structure/#compiler-annotations) in the following form tells the compiler which of the versions of Pine Script® the script is written in:

[Pine Script®](https://tradingview.com/pine-script-docs)

```pine
//@version=6
```

-   The version number is a number from 1 to 6.
-   The compiler annotation is not mandatory. When omitted, version 1 is assumed. It is strongly recommended to always use the latest version of the language.
-   While it is synctactically correct to place the version compiler annotation anywhere in the script, it is much more useful to readers when it appears at the top of the script.

Notable changes to the current version of Pine Script are documented in the [Release notes](https://www.tradingview.com/pine-script-docs/release-notes/).

## Declaration statement

All Pine scripts must contain one declaration statement, which is a call to one of these functions:

-   [indicator()](https://www.tradingview.com/pine-script-reference/v6/#fun_indicator)
-   [strategy()](https://www.tradingview.com/pine-script-reference/v6/#fun_strategy)
-   [library()](https://www.tradingview.com/pine-script-reference/v6/#fun_library)

The declaration statement:

-   Identifies the type of the script, which in turn dictates which content is allowed in it, and how it can be used and executed.
-   Sets key properties of the script such as its name, where it will appear when it is added to a chart, the precision and format of the values it displays, and certain values that govern its runtime behavior, such as the maximum number of drawing objects it will display on the chart. With strategies, the properties include parameters that control backtesting, such as initial capital, commission, slippage, etc.

Each script type has distinct basic requirements. Scripts that do not meet these criteria cause a compilation error:

-   Indicators must call at least one function that creates a script output, such as [plot()](https://www.tradingview.com/pine-script-reference/v6/#fun_plot), [plotshape()](https://www.tradingview.com/pine-script-reference/v6/#fun_plotshape), [barcolor()](https://www.tradingview.com/pine-script-reference/v6/#fun_barcolor), [line.new()](https://www.tradingview.com/pine-script-reference/v6/#fun_line.new), [log.info()](https://www.tradingview.com/pine-script-reference/v6/#fun_log.info), [alert()](https://www.tradingview.com/pine-script-reference/v6/#fun_alert), etc.
-   [Strategies](https://www.tradingview.com/pine-script-docs/concepts/strategies/) must call at least one [order placement command](https://www.tradingview.com/pine-script-docs/concepts/strategies/#order-placement-and-cancellation) or other output function.
-   [Libraries](https://www.tradingview.com/pine-script-docs/concepts/libraries/) must [export](https://www.tradingview.com/pine-script-reference/v6/#kw_export) at least one user-defined [function](https://www.tradingview.com/pine-script-docs/language/user-defined-functions/), [method](https://www.tradingview.com/pine-script-docs/language/methods/#user-defined-methods), [type](https://www.tradingview.com/pine-script-docs/language/type-system/#user-defined-types), or [enum](https://www.tradingview.com/pine-script-docs/language/enums/).

## Code

Lines in a script that are not [comments](https://www.tradingview.com/pine-script-docs/language/script-structure/#comments) or [compiler annotations](https://www.tradingview.com/pine-script-docs/language/script-structure/#compiler-annotations) are *statements*, which implement the script’s algorithm. A statement can be one of these:

-   [variable declaration](https://www.tradingview.com/pine-script-docs/language/variable-declarations/)
-   [variable reassignment](https://www.tradingview.com/pine-script-docs/language/variable-declarations/#variable-reassignment)
-   [function definition](https://www.tradingview.com/pine-script-docs/language/user-defined-functions/#structure-and-syntax)
-   [built-in function call](https://www.tradingview.com/pine-script-docs/language/built-ins/#built-in-functions), [user-defined function call](https://www.tradingview.com/pine-script-docs/language/user-defined-functions/) or [a library function call](https://www.tradingview.com/pine-script-docs/concepts/libraries/#using-a-library)
-   [if](https://www.tradingview.com/pine-script-reference/v6/#kw_if), [for](https://www.tradingview.com/pine-script-reference/v6/#kw_for), [while](https://www.tradingview.com/pine-script-reference/v6/#kw_while), [switch](https://www.tradingview.com/pine-script-reference/v6/#kw_switch), [type](https://www.tradingview.com/pine-script-reference/v6/#kw_type), or [enum](https://www.tradingview.com/pine-script-reference/v6/#kw_enum) *structure*.

Statements can be arranged in multiple ways:

-   Some statements can be expressed in one line, like most variable declarations, lines containing only a function call or single-line function declarations. Lines can also be [wrapped](https://www.tradingview.com/pine-script-docs/language/script-structure/#line-wrapping) (continued on multiple lines). Multiple one-line statements can be concatenated on a single line by using the comma as a separator.
-   Others statements such as structures or multiline function definitions always require multiple lines because they require a *local block*. A local block must be indented by a tab or four spaces. Each local block defines a distinct *local scope*.
-   Statements in the *global scope* of the script (i.e., which are not part of local blocks) cannot begin with white space (a space or a tab). Their first character must also be the line’s first character. Lines beginning in a line’s first position become by definition part of the script’s *global scope*.

A simple valid Pine Script indicator can be generated in the Pine Script Editor by using the “Open” button and choosing “New blank indicator”:

[Pine Script®](https://tradingview.com/pine-script-docs)

```pine
//@version=6
indicator("My Script")
plot(close)
```

This indicator includes three local blocks, one in the `barIsUp()` function declaration, and two in the variable declaration using an [if](https://www.tradingview.com/pine-script-reference/v6/#kw_if) structure:

[Pine Script®](https://tradingview.com/pine-script-docs)

```pine
//@version=6

indicator("", "", true)    // Declaration statement (global scope)

barIsUp() =>    // Function declaration (global scope)
    close > open    // Local block (local scope)

plotColor = if barIsUp()  // Variable declaration (global scope)
    color.green     // Local block (local scope)
else
    color.red       // Local block (local scope)

bgcolor(color.new(plotColor, 70))   // Call to a built-in function  (global scope)
```

You can bring up a simple Pine Script strategy by selecting “New blank strategy” instead:

[Pine Script®](https://tradingview.com/pine-script-docs)

```pine
//@version=6
strategy("My Strategy", overlay=true, margin_long=100, margin_short=100)

longCondition = ta.crossover(ta.sma(close, 14), ta.sma(close, 28))
if (longCondition)
    strategy.entry("My Long Entry Id", strategy.long)

shortCondition = ta.crossunder(ta.sma(close, 14), ta.sma(close, 28))
if (shortCondition)
    strategy.entry("My Short Entry Id", strategy.short)
```

## Comments

Double slashes (`//`) define comments in Pine Script. Comments can begin anywhere on the line. They can also follow Pine Script code on the same line:

[Pine Script®](https://tradingview.com/pine-script-docs)

```pine
//@version=6
indicator("")
// This line is a comment
a = close // This is also a comment
plot(a)
```

The Pine Editor has a keyboard shortcut to comment/uncomment lines: `ctrl` + `/`. You can use it on multiple lines by highlighting them first.

## Line wrapping

Long lines can be split on multiple lines, or “wrapped”. Wrapped lines must be indented with any number of spaces, provided it’s not a multiple of four (those boundaries are used to indent local blocks):

[Pine Script®](https://tradingview.com/pine-script-docs)

```pine
a = open + high + low + close
```

may be wrapped as:

[Pine Script®](https://tradingview.com/pine-script-docs)

```pine
a = open +
      high +
          low +
             close
```

A long [plot()](https://www.tradingview.com/pine-script-reference/v6/#fun_plot) call may be wrapped as:

[Pine Script®](https://tradingview.com/pine-script-docs)

```pine
plot(ta.correlation(src, ovr, length),
   color = color.new(color.purple, 40),
   style = plot.style_area,
   trackprice = true)
```

Expressions inside *local* code blocks can also use line wrapping. However, because the code in a local block requires indentation by four spaces or a tab, we recommend using a *larger* indentation that is not a multiple of four spaces for the wrapped lines inside the block. For example:

[Pine Script®](https://tradingview.com/pine-script-docs)

```pine
upDown(float s) =>
    var int ud = 0
    bool isEqual   = s == s[1]
    bool isGrowing = s > s[1]
    ud := isEqual ?
           0 :
           isGrowing ?
               (ud <= 0 ?
                     1 :
                   ud + 1) :
               (ud >= 0 ?
                   -1 :
                   ud - 1)
```

Wrapped lines can also include [comments](https://www.tradingview.com/pine-script-docs/language/script-structure/#comments):

[Pine Script®](https://tradingview.com/pine-script-docs)

```pine
//@version=6
indicator("")
c = open > close ? color.red :
  high > high[1] ? color.lime : // A comment
  low < low[1] ? color.blue : color.black
bgcolor(c)
```

## Compiler annotations

Compiler annotations are [comments](https://www.tradingview.com/pine-script-docs/language/script-structure/#comments) that issue special instructions for a script:

-   `//@version=` specifies the PineScript version that the compiler will use. The number in this annotation should not be confused with the script’s version number, which updates on every saved change to the code.
-   `//@description` sets a custom description for scripts that use the [library()](https://www.tradingview.com/pine-script-reference/v6/#fun_library) declaration statement.
-   `//@function`, `//@param` and `//@returns` add custom descriptions for a [user-defined function](https://www.tradingview.com/pine-script-docs/language/user-defined-functions/) or [method](https://www.tradingview.com/pine-script-docs/language/methods/), its parameters, and its result when placed above the function declaration.
-   `//@type` adds a custom description for a [user-defined type (UDT)](https://www.tradingview.com/pine-script-docs/language/type-system/#user-defined-types) when placed above the type declaration.
-   `//@enum` adds a custom description for an [enum types](https://www.tradingview.com/pine-script-docs/language/type-system/#enum-types) when placed above the enum declaration.
-   `//@field` adds a custom description for the field of a [user-defined type (UDT)](https://www.tradingview.com/pine-script-docs/language/type-system/#user-defined-types) or an [enum types](https://www.tradingview.com/pine-script-docs/language/type-system/#enum-types) when placed above the type or enum declaration.
-   `//@variable` adds a custom description for a variable when placed above its declaration.
-   `//@strategy_alert_message` provides a default message for strategy scripts to pre-fill the “Message” field in the alert creation dialog.

The Pine Editor also features two specialized annotations, `//#region` and `//#endregion`, that create *collapsible* code regions. Clicking the dropdown arrow next to a `//#region` line collapses all the code between that line and the nearest `//#endregion` annotation below it.

This example draws a triangle using three interactively selected points on the chart. The script illustrates how one can use compiler and Editor annotations to document code and make it easier to navigate:

![image](https://www.tradingview.com/pine-script-docs/_astro/ScriptStructure-CompilerAnnotations01.CdT2JzaQ_2sKSpL.webp)

[Pine Script®](https://tradingview.com/pine-script-docs)

```pine
//@version=6
indicator("Triangle", "", true)

//#region ———————————————————— Constants and inputs

int   TIME_DEFAULT  = 0
float PRICE_DEFAULT = 0.0

x1Input = input.time(TIME_DEFAULT,   "Point 1", inline = "1", confirm = true)
y1Input = input.price(PRICE_DEFAULT, "",        inline = "1", tooltip = "Pick point 1", confirm = true)
x2Input = input.time(TIME_DEFAULT,   "Point 2", inline = "2", confirm = true)
y2Input = input.price(PRICE_DEFAULT, "",        inline = "2", tooltip = "Pick point 2", confirm = true)
x3Input = input.time(TIME_DEFAULT,   "Point 3", inline = "3", confirm = true)
y3Input = input.price(PRICE_DEFAULT, "",        inline = "3", tooltip = "Pick point 3", confirm = true)
//#endregion

//#region ———————————————————— Types and functions

// @type            Used to represent the coordinates and color to draw a triangle.
// @field time1     Time of first point.
// @field time2     Time of second point.
// @field time3     Time of third point.
// @field price1    Price of first point.
// @field price2    Price of second point.
// @field price3    Price of third point.
// @field lineColor Color to be used to draw the triangle lines.
type Triangle
    int   time1
    int   time2
    int   time3
    float price1
    float price2
    float price3
    color lineColor

//@function Draws a triangle using the coordinates of the `t` object.
//@param t  (Triangle) Object representing the triangle to be drawn.
//@returns  The ID of the last line drawn.
drawTriangle(Triangle t) =>
    line.new(t.time1, t.price1, t.time2, t.price2, xloc = xloc.bar_time, color = t.lineColor)
    line.new(t.time2, t.price2, t.time3, t.price3, xloc = xloc.bar_time, color = t.lineColor)
    line.new(t.time1, t.price1, t.time3, t.price3, xloc = xloc.bar_time, color = t.lineColor)
//#endregion

//#region ———————————————————— Calculations

// Draw the triangle only once on the last historical bar.
if barstate.islastconfirmedhistory
    //@variable Used to hold the Triangle object to be drawn.
    Triangle triangle = Triangle.new()

    triangle.time1  := x1Input
    triangle.time2  := x2Input
    triangle.time3  := x3Input
    triangle.price1 := y1Input
    triangle.price2 := y2Input
    triangle.price3 := y3Input
    triangle.lineColor := color.purple

    drawTriangle(triangle)
//#endregion
```
