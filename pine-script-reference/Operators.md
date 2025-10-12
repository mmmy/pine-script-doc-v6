# Operators

### -

Subtraction or unary minus. Applicable to numerical expressions.

**SYNTAX**

```
expr1 - expr2
```

**RETURNS**

Returns integer or float value, or series of values:

Binary - returns expr1 minus expr2.

Unary - returns the negation of expr.

**REMARKS**

You may use arithmetic operators with numbers as well as with series variables. In case of usage with series the operators are applied elementwise.

---

### -=

Subtraction assignment. Applicable to numerical expressions.

**SYNTAX**

```
expr1 -= expr2
```

**EXAMPLE**

```pine
//@version=6
indicator("-=")
// Equals to expr1 = expr1 - expr2.
a = 2
b = 3
a -= b
// Result: a = -1.
plot(a)
```

**RETURNS**

Integer or float value, or series of values.

---

### :=

Reassignment operator. It is used to assign a new value to a previously declared variable.

**SYNTAX**

```
<var_name> := <new_value>
```

**EXAMPLE**

```pine
//@version=6
indicator("My script")

myVar = 10

if close > open
    // Modifies the existing global scope `myVar` variable by changing its value from 10 to 20.
    myVar := 20
    // Creates a new `myVar` variable local to the `if` condition and unreachable from the global scope.
    // Does not affect the `myVar` declared in global scope.
    myVar = 30

plot(myVar)
```

---

### !=

Inequality operator. Returns true if the operands are considered not equal, and false otherwise. This operator is compatible with all value types, including "int", "float", "bool", "color", and "string". The operator can also compare two line or label IDs.

**SYNTAX**

```
expr1 != expr2
```

**RETURNS**

Boolean value, or series of boolean values.

**REMARKS**

This operator rounds "float" operands to nine fractional digits.

---

### ?:

Ternary conditional operator.

**SYNTAX**

```
expr1 ? expr2 : expr3
```

**EXAMPLE**

```pine
//@version=6
indicator("?:")
// Draw circles at the bars where open crosses close
s2 = ta.cross(open, close) ? math.avg(open,close) : na
plot(s2, style=plot.style_circles, linewidth=2, color=color.red)

// Combination of ?: operators for 'switch'-like logic
c = timeframe.isintraday ? color.red : timeframe.isdaily ? color.green : timeframe.isweekly ? color.blue : color.gray
plot(hl2, color=c)
```

**RETURNS**

expr2 if expr1 is evaluated to true, expr3 otherwise. Zero value (0 and also NaN, +Infinity, -Infinity) is considered to be false, any other value is true.

**REMARKS**

Use na for 'else' branch if you do not need it.

You can combine two or more ?: operators to achieve the equivalent of a 'switch'-like statement (see examples above).

You may use arithmetic operators with numbers as well as with series variables. In case of usage with series the operators are applied elementwise.

**SEE ALSO**

na

---

### []

Series subscript. Provides access to previous values of series expr1. expr2 is the number of bars back, and must be numerical. Floats will be rounded down.

**SYNTAX**

```
expr1[expr2]
```

**EXAMPLE**

```pine
//@version=6
indicator("[]")
// [] can be used to "save" variable value between bars
a = 0.0 // declare `a`
a := a[1] // immediately set current value to the same as previous. `na` in the beginning of history
if high == low // if some condition - change `a` value to another
    a := low
plot(a)
```

**RETURNS**

A series of values.

**SEE ALSO**

math.floor

---

### *

Multiplication. Applicable to numerical expressions.

**SYNTAX**

```
expr1 * expr2
```

**RETURNS**

Integer or float value, or series of values.

---

### *=

Multiplication assignment. Applicable to numerical expressions.

**SYNTAX**

```
expr1 *= expr2
```

**EXAMPLE**

```pine
//@version=6
indicator("*=")
// Equals to expr1 = expr1 * expr2.
a = 2
b = 3
a *= b
// Result: a = 6.
plot(a)
```

**RETURNS**

Integer or float value, or series of values.

---

### /

Division. Applicable to numerical expressions.

**SYNTAX**

```
expr1 / expr2
```

**RETURNS**

Integer or float value, or series of values.

---

### /=

Division assignment. Applicable to numerical expressions.

**SYNTAX**

```
expr1 /= expr2
```

**EXAMPLE**

```pine
//@version=6
indicator("/=")
// Equals to expr1 = expr1 / expr2.
float a = 3.0
b = 3
a /= b
// Result: a = 1.
plot(a)
```

**RETURNS**

Integer or float value, or series of values.

---

### %

Modulo (integer remainder). Applicable to numerical expressions.

**SYNTAX**

```
expr1 % expr2
```

**RETURNS**

Integer or float value, or series of values.

**REMARKS**

In Pine Script®, when the integer remainder is calculated, the quotient is truncated, i.e. rounded towards the lowest absolute value. The resulting value will have the same sign as the dividend.

Example: -1 % 9 = -1 - 9 * int(-1/9) = -1 - 9 * int(-0.111) = -1 - 9 * 0 = -1.

---

### %=

Modulo assignment. Applicable to numerical expressions.

**SYNTAX**

```
expr1 %= expr2
```

**EXAMPLE**

```pine
//@version=6
indicator("%=")
// Equals to expr1 = expr1 % expr2.
a = 3
b = 3
a %= b
// Result: a = 0.
plot(a)
```

**RETURNS**

Integer or float value, or series of values.

---

### +

Addition or unary plus. Applicable to numerical expressions or strings.

**SYNTAX**

```
expr1 + expr2
```

**RETURNS**

Binary + for strings returns concatenation of expr1 and expr2

For numbers returns integer or float value, or series of values:

Binary + returns expr1 plus expr2.

Unary + returns expr (does nothing added just for the symmetry with the unary - operator).

**REMARKS**

You may use arithmetic operators with numbers as well as with series variables. In case of usage with series the operators are applied elementwise.

---

### +=

Addition assignment. Applicable to numerical expressions or strings.

**SYNTAX**

```
expr1 += expr2
```

**EXAMPLE**

```pine
//@version=6
indicator("+=")
// Equals to expr1 = expr1 + expr2.
a = 2
b = 3
a += b
// Result: a = 5.
plot(a)
```

**RETURNS**

For strings returns concatenation of expr1 and expr2. For numbers returns integer or float value, or series of values.

**REMARKS**

You may use arithmetic operators with numbers as well as with series variables. In case of usage with series the operators are applied elementwise.

---

### <

Less than. Applicable to numerical expressions.

**SYNTAX**

```
expr1 < expr2
```

**RETURNS**

Boolean value, or series of boolean values.

---

### <=

Less than or equal to. Applicable to numerical expressions.

**SYNTAX**

```
expr1 <= expr2
```

**RETURNS**

Boolean value, or series of boolean values.

---

### =

Assignment operator. Assigns an initial value or reference to a declared variable. It means this is a new variable, and it starts with this value.

**SYNTAX**

```
<var_name> := <initial_value>
```

**EXAMPLE**

```pine
//@version=6
indicator("`=` showcase")
// The following are all valid variable declarations.
i = 1
MS_IN_ONE_MINUTE = 1000 * 60
showPlotInput = input.bool(true, "Show plots")
pHi = ta.pivothigh(5, 5)
plotColor = color.green

plot(pHi, color = plotColor, display = showPlotInput ? display.all : display.none, precision = i)
```

---

### ==

Equality operator. Returns true if the operands are considered equal, and false otherwise. This operator is compatible with all value types, including "int", "float", "bool", "color", and "string". The operator can also compare two line or label IDs.

**SYNTAX**

```
expr1 == expr2
```

**RETURNS**

Boolean value, or series of boolean values.

**REMARKS**

This operator rounds "float" operands to nine fractional digits.

---

### =>

The '=>' operator is used in user-defined function declarations and in switch statements.

The function declaration syntax is:

**SYNTAX**

```
<identifier>([<parameter_name>[=<default_value>]], ...) =>
    <local_block>
    <function_result>
```

A <local_block> is zero or more Pine Script® statements.

The <function_result> is a variable, an expression, or a tuple.

**EXAMPLE**

```pine
//@version=6
indicator("=>")
// single-line function
f1(x, y) => x + y
// multi-line function
f2(x, y) =>
    sum = x + y
    sumChange = ta.change(sum, 10)
    // Function automatically returns the last expression used in it
plot(f1(30, 8) + f2(1, 3))
```

**REMARKS**

You can learn more about user-defined functions in the User Manual's pages on Declaring functions and Libraries.

---

### >

Greater than. Applicable to numerical expressions.

**SYNTAX**

```
expr1 > expr2
```

**RETURNS**

Boolean value, or series of boolean values.

---

### >=

Greater than or equal to. Applicable to numerical expressions.

**SYNTAX**

```
expr1 >= expr2
```

**RETURNS**

Boolean value, or series of boolean values.
