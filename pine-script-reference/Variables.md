# Variables

### ask

The ask price at the time of the current tick, which represents the lowest price an active seller will accept for the instrument at its current value. This information is available only on the "1T" timeframe. On other timeframes, the variable's value is na.

**TYPE**

series float

**REMARKS**

If the bid/ask values change since the last tick but no new trades are made, these changes will not be reflected in the value of this variable. It is only updated on new ticks.

**SEE ALSO**

open, high, low, volume, time, hl2, hlc3, hlcc4, ohlc4, bid

---

### bar_index

Current bar index. Numbering is zero-based, index of the first bar is 0.

**TYPE**

series int

**EXAMPLE**

```pine
//@version=6
indicator("bar_index")
plot(bar_index)
plot(bar_index > 5000 ? close : 0)
```

**REMARKS**

Note that bar_index has replaced n variable in version 4.

Note that bar indexing starts from 0 on the first historical bar.

Please note that using this variable/function can cause indicator repainting.

**SEE ALSO**

last_bar_index, barstate.isfirst, barstate.islast, barstate.isrealtime

---

### barstate.isconfirmed

Returns true if the script is calculating the last (closing) update of the current bar. The next script calculation will be on the new bar data.

**TYPE**

series bool

**REMARKS**

Pine Script® code that uses this variable could calculate differently on history and real-time data.

It is NOT recommended to use barstate.isconfirmed in request.security expression. Its value requested from request.security is unpredictable.

**SEE ALSO**

barstate.isfirst, barstate.islast, barstate.ishistory, barstate.isrealtime, barstate.isnew, barstate.islastconfirmedhistory

---

### barstate.isfirst

Returns true if current bar is first bar in barset, false otherwise.

**TYPE**

series bool

**REMARKS**

Pine Script® code that uses this variable could calculate differently on history and real-time data.

Please note that using this variable/function can cause indicator repainting.

**SEE ALSO**

barstate.islast, barstate.ishistory, barstate.isrealtime, barstate.isnew, barstate.isconfirmed, barstate.islastconfirmedhistory

---

### barstate.ishistory

Returns true if current bar is a historical bar, false otherwise.

**TYPE**

series bool

**REMARKS**

Pine Script® code that uses this variable could calculate differently on history and real-time data.

Please note that using this variable/function can cause indicator repainting.

**SEE ALSO**

barstate.isfirst, barstate.islast, barstate.isrealtime, barstate.isnew, barstate.isconfirmed, barstate.islastconfirmedhistory

---

### barstate.islast

Returns true if current bar is the last bar in barset, false otherwise. This condition is true for all real-time bars in barset.

**TYPE**

series bool

**REMARKS**

Pine Script® code that uses this variable could calculate differently on history and real-time data.

Please note that using this variable/function can cause indicator repainting.

**SEE ALSO**

barstate.isfirst, barstate.ishistory, barstate.isrealtime, barstate.isnew, barstate.isconfirmed, barstate.islastconfirmedhistory

---

### barstate.islastconfirmedhistory

Returns true if script is executing on the dataset's last bar when market is closed, or script is executing on the bar immediately preceding the real-time bar, if market is open. Returns false otherwise.

**TYPE**

series bool

**REMARKS**

Pine Script® code that uses this variable could calculate differently on history and real-time data.

Please note that using this variable/function can cause indicator repainting.

**SEE ALSO**

barstate.isfirst, barstate.islast, barstate.ishistory, barstate.isrealtime, barstate.isnew

---

### barstate.isnew

Returns true if script is currently calculating on new bar, false otherwise. This variable is true when calculating on historical bars or on first update of a newly generated real-time bar.

**TYPE**

series bool

**REMARKS**

Pine Script® code that uses this variable could calculate differently on history and real-time data.

Please note that using this variable/function can cause indicator repainting.

**SEE ALSO**

barstate.isfirst, barstate.islast, barstate.ishistory, barstate.isrealtime, barstate.isconfirmed, barstate.islastconfirmedhistory

---

### barstate.isrealtime

Returns true if current bar is a real-time bar, false otherwise.

**TYPE**

series bool

**REMARKS**

Pine Script® code that uses this variable could calculate differently on history and real-time data.

Please note that using this variable/function can cause indicator repainting.

**SEE ALSO**

barstate.isfirst, barstate.islast, barstate.ishistory, barstate.isnew, barstate.isconfirmed, barstate.islastconfirmedhistory

---

### bid

The bid price at the time of the current tick, which represents the highest price an active buyer is willing to pay for the instrument at its current value. This information is available only on the "1T" timeframe. On other timeframes, the variable's value is na.

**TYPE**

series float

**REMARKS**

If the bid/ask values change since the last tick but no new trades are made, these changes will not be reflected in the value of this variable. It is only updated on new ticks.

**SEE ALSO**

open, high, low, volume, time, hl2, hlc3, hlcc4, ohlc4, ask

---

### box.all

Returns an array filled with all the current boxes drawn by the script.

**TYPE**

array<box>

**EXAMPLE**

```pine
//@version=6
indicator("box.all")
//delete all boxes
box.new(time, open, time + 60 * 60 * 24, close, xloc=xloc.bar_time, border_style=line.style_dashed)
a_allBoxes = box.all
if array.size(a_allBoxes) > 0
    for i = 0 to array.size(a_allBoxes) - 1
        box.delete(array.get(a_allBoxes, i))
```

**REMARKS**

The array is read-only. Index zero of the array is the ID of the oldest object on the chart.

**SEE ALSO**

box.new, line.all, label.all, table.all

---

### chart.bg_color

Returns the color of the chart's background from the "Chart settings/Appearance/Background" field. When a gradient is selected, the middle point of the gradient is returned.

**TYPE**

input color

**SEE ALSO**

chart.fg_color

---

### chart.fg_color

Returns a color providing optimal contrast with chart.bg_color.

**TYPE**

input color

**SEE ALSO**

chart.bg_color

---

### chart.is_heikinashi

**TYPE**

simple bool

**RETURNS**

Returns true if the chart type is Heikin Ashi, false otherwise.

**SEE ALSO**

chart.is_renko, chart.is_linebreak, chart.is_kagi, chart.is_pnf, chart.is_range

---

### chart.is_kagi

**TYPE**

simple bool

**RETURNS**

Returns true if the chart type is Kagi, false otherwise.

**SEE ALSO**

chart.is_renko, chart.is_linebreak, chart.is_heikinashi, chart.is_pnf, chart.is_range

---

### chart.is_linebreak

**TYPE**

simple bool

**RETURNS**

Returns true if the chart type is Line break, false otherwise.

**SEE ALSO**

chart.is_renko, chart.is_heikinashi, chart.is_kagi, chart.is_pnf, chart.is_range

---

### chart.is_pnf

**TYPE**

simple bool

**RETURNS**

Returns true if the chart type is Point & figure, false otherwise.

**SEE ALSO**

chart.is_renko, chart.is_linebreak, chart.is_kagi, chart.is_heikinashi, chart.is_range

---

### chart.is_range

**TYPE**

simple bool

**RETURNS**

Returns true if the chart type is Range, false otherwise.

**SEE ALSO**

chart.is_renko, chart.is_linebreak, chart.is_kagi, chart.is_pnf, chart.is_heikinashi

---

### chart.is_renko

**TYPE**

simple bool

**RETURNS**

Returns true if the chart type is Renko, false otherwise.

**SEE ALSO**

chart.is_heikinashi, chart.is_linebreak, chart.is_kagi, chart.is_pnf, chart.is_range

---

### chart.is_standard

**TYPE**

simple bool

**RETURNS**

Returns true if the chart type is not one of the following: Renko, Kagi, Line break, Point & figure, Range, Heikin Ashi; false otherwise.

**SEE ALSO**

chart.is_renko, chart.is_linebreak, chart.is_kagi, chart.is_pnf, chart.is_range, chart.is_heikinashi

---

### chart.left_visible_bar_time

The time of the leftmost bar currently visible on the chart.

**TYPE**

input int

**REMARKS**

Scripts using this variable will automatically re-execute when its value updates to reflect changes in the chart, which can be caused by users scrolling the chart, or new real-time bars.

Alerts created on a script that includes this variable will only use the value assigned to the variable at the moment of the alert's creation, regardless of whether the value changes afterward, which may lead to repainting.

**SEE ALSO**

chart.right_visible_bar_time

---

### chart.right_visible_bar_time

The time of the rightmost bar currently visible on the chart.

**TYPE**

input int

**REMARKS**

Scripts using this variable will automatically re-execute when its value updates to reflect changes in the chart, which can be caused by users scrolling the chart, or new real-time bars.

Alerts created on a script that includes this variable will only use the value assigned to the variable at the moment of the alert's creation, regardless of whether the value changes afterward, which may lead to repainting.

**SEE ALSO**

chart.left_visible_bar_time

---

### close

Close price of the current bar when it has closed, or last traded price of a yet incomplete, realtime bar.

**TYPE**

series float

**REMARKS**

Previous values may be accessed with square brackets operator [], e.g. close[1], close[2].

**SEE ALSO**

open, high, low, volume, time, hl2, hlc3, hlcc4, ohlc4, ask, bid

---

### dayofmonth

The day number of the month, in the exchange time zone, calculated from the bar's opening UNIX timestamp.

**TYPE**

series int

**REMARKS**

This variable always references the day number corresponding to the bar's opening time. Consequently, for symbols with overnight sessions (e.g., "EURUSD", where the "Monday" session starts on Sunday at 17:00 in exchange time), the value may represent a day from the previous week rather than the session's primary trading day.

**SEE ALSO**

dayofmonth, dayofweek, weekofyear, time, year, month, hour, minute, second

---

### dayofweek

The day number of the week, in the exchange time zone, calculated from the bar's opening UNIX timestamp.

**TYPE**

series int

**REMARKS**

This variable always references the day number corresponding to the bar's opening time. Consequently, for symbols with overnight sessions (e.g., "EURUSD", where the "Monday" session starts on Sunday at 17:00 in exchange time), the value may represent a day from the previous week rather than the session's primary trading day.

You can use dayofweek.sunday, dayofweek.monday, dayofweek.tuesday, dayofweek.wednesday, dayofweek.thursday, dayofweek.friday and dayofweek.saturday variables for comparisons.

**SEE ALSO**

dayofweek, time, year, month, weekofyear, dayofmonth, hour, minute, second

---

### dividends.future_amount

Returns the payment amount of the upcoming dividend in the currency of the current instrument, or na if this data isn't available.

**TYPE**

series float

**REMARKS**

This value is only fetched once during the script's initial calculation. The variable will return the same value until the script is recalculated, even after the expected Payment date of the next dividend.

---

### dividends.future_ex_date

Returns the Ex-dividend date (Ex-date) of the current instrument's next dividend payment, or na if this data isn't available. Ex-dividend date signifies when investors are no longer entitled to a payout from the most recent dividend. Only those who purchased shares before this day are entitled to the dividend payment.

**TYPE**

series int

**RETURNS**

UNIX time, expressed in milliseconds.

**REMARKS**

This value is only fetched once during the script's initial calculation. The variable will return the same value until the script is recalculated, even after the expected Payment date of the next dividend.

---

### dividends.future_pay_date

Returns the Payment date (Pay date) of the current instrument's next dividend payment, or na if this data isn't available. Payment date signifies the day when eligible investors will receive the dividend payment.

**TYPE**

series int

**RETURNS**

UNIX time, expressed in milliseconds.

**REMARKS**

This value is only fetched once during the script's initial calculation. The variable will return the same value until the script is recalculated, even after the expected Payment date of the next dividend.

---

### earnings.future_eps

Returns the estimated Earnings per Share of the next earnings report in the currency of the instrument, or na if this data isn't available.

**TYPE**

series float

**REMARKS**

This value is only fetched once during the script's initial calculation. The variable will return the same value until the script is recalculated, even after the expected time of the next earnings report.

**SEE ALSO**

request.earnings

---

### earnings.future_period_end_time

Checks the data for the next earnings report and returns the UNIX timestamp of the day when the financial period covered by those earnings ends, or na if this data isn't available.

**TYPE**

series int

**RETURNS**

UNIX time, expressed in milliseconds.

**REMARKS**

This value is only fetched once during the script's initial calculation. The variable will return the same value until the script is recalculated, even after the expected time of the next earnings report.

**SEE ALSO**

request.earnings

---

### earnings.future_revenue

Returns the estimated Revenue of the next earnings report in the currency of the instrument, or na if this data isn't available.

**TYPE**

series float

**REMARKS**

This value is only fetched once during the script's initial calculation. The variable will return the same value until the script is recalculated, even after the expected time of the next earnings report.

**SEE ALSO**

request.earnings

---

### earnings.future_time

Returns a UNIX timestamp indicating the expected time of the next earnings report, or na if this data isn't available.

**TYPE**

series int

**RETURNS**

UNIX time, expressed in milliseconds.

**REMARKS**

This value is only fetched once during the script's initial calculation. The variable will return the same value until the script is recalculated, even after the expected time of the next earnings report.

**SEE ALSO**

request.earnings

---

### high

Current high price.

**TYPE**

series float

**REMARKS**

Previous values may be accessed with square brackets operator [], e.g. high[1], high[2].

**SEE ALSO**

open, low, close, volume, time, hl2, hlc3, hlcc4, ohlc4, ask, bid

---

### hl2

Is a shortcut for (high + low)/2

**TYPE**

series float

**SEE ALSO**

open, high, low, close, volume, time, hlc3, hlcc4, ohlc4, ask, bid

---

### hlc3

Is a shortcut for (high + low + close)/3

**TYPE**

series float

**SEE ALSO**

open, high, low, close, volume, time, hl2, hlcc4, ohlc4, ask, bid

---

### hlcc4

Is a shortcut for (high + low + close + close)/4

**TYPE**

series float

**SEE ALSO**

open, high, low, close, volume, time, hl2, hlc3, ohlc4, ask, bid

---

### hour

Current bar hour in exchange timezone.

**TYPE**

series int

**SEE ALSO**

hour, time, year, month, weekofyear, dayofmonth, dayofweek, minute, second

---

### label.all

Returns an array filled with all the current labels drawn by the script.

**TYPE**

array<label>

**EXAMPLE**

```pine
//@version=6
indicator("label.all")
//delete all labels
label.new(bar_index, close)
a_allLabels = label.all
if array.size(a_allLabels) > 0
    for i = 0 to array.size(a_allLabels) - 1
        label.delete(array.get(a_allLabels, i))
```

**REMARKS**

The array is read-only. Index zero of the array is the ID of the oldest object on the chart.

**SEE ALSO**

label.new, line.all, box.all, table.all

---

### last_bar_index

Bar index of the last chart bar. Bar indices begin at zero on the first bar.

**TYPE**

series int

**EXAMPLE**

```pine
//@version=6
strategy("Mark Last X Bars For Backtesting", overlay = true, calc_on_every_tick = true)
lastBarsFilterInput = input.int(100, "Bars Count:")
// Here, we store the 'last_bar_index' value that is known from the beginning of the script's calculation.
// The 'last_bar_index' will change when new real-time bars appear, so we declare 'lastbar' with the 'var' keyword.
var lastbar = last_bar_index
// Check if the current bar_index is 'lastBarsFilterInput' removed from the last bar on the chart, or the chart is traded in real-time.
allowedToTrade = (lastbar - bar_index <= lastBarsFilterInput) or barstate.isrealtime
bgcolor(allowedToTrade ? color.new(color.green, 80) : na)
```

**RETURNS**

Last historical bar index for closed markets, or the real-time bar index for open markets.

**REMARKS**

Please note that using this variable can cause indicator repainting.

**SEE ALSO**

bar_index, last_bar_time, barstate.ishistory, barstate.isrealtime

---

### last_bar_time

Time in UNIX format of the last chart bar. It is the number of milliseconds that have elapsed since 00:00:00 UTC, 1 January 1970.

**TYPE**

series int

**REMARKS**

Please note that using this variable/function can cause indicator repainting.

Note that this variable returns the timestamp based on the time of the bar's open.

**SEE ALSO**

time, timenow, timestamp, last_bar_index

---

### line.all

Returns an array filled with all the current lines drawn by the script.

**TYPE**

array<line>

**EXAMPLE**

```pine
//@version=6
indicator("line.all")
//delete all lines
line.new(bar_index - 10, close, bar_index, close)
a_allLines = line.all
if array.size(a_allLines) > 0
    for i = 0 to array.size(a_allLines) - 1
        line.delete(array.get(a_allLines, i))
```

**REMARKS**

The array is read-only. Index zero of the array is the ID of the oldest object on the chart.

**SEE ALSO**

line.new, label.all, box.all, table.all

---

### linefill.all

Returns an array filled with all the current linefill objects drawn by the script.

**TYPE**

array<linefill>

**REMARKS**

The array is read-only. Index zero of the array is the ID of the oldest object on the chart.

---

### low

Current low price.

**TYPE**

series float

**REMARKS**

Previous values may be accessed with square brackets operator [], e.g. low[1], low[2].

**SEE ALSO**

open, high, close, volume, time, hl2, hlc3, hlcc4, ohlc4, ask, bid

---

### minute

Current bar minute in exchange timezone.

**TYPE**

series int

**SEE ALSO**

minute, time, year, month, weekofyear, dayofmonth, dayofweek, hour, second

---

### month

Current bar month in exchange timezone.

**TYPE**

series int

**REMARKS**

Note that this variable returns the month based on the time of the bar's open. For overnight sessions (e.g. EURUSD, where Monday session starts on Sunday, 17:00) this value can be lower by 1 than the month of the trading day.

**SEE ALSO**

month, time, year, weekofyear, dayofmonth, dayofweek, hour, minute, second

---

### na

A keyword signifying "not available", indicating that a variable has no assigned value.

**TYPE**

simple na

**EXAMPLE**

```pine
//@version=6
indicator("na")
// CORRECT
// Plot no value when on bars zero to nine. Plot `close` on other bars.
plot(bar_index < 10 ? na : close)
// CORRECT ALTERNATIVE
// Initialize `a` to `na`. Reassign `close` to `a` on bars 10 and later.
float a = na
if bar_index >= 10
    a := close
plot(a)

// INCORRECT
// Trying to test the preceding bar's `close` for `na`.
// The next line, if uncommented, will cause a compilation error, because direct comparison with `na` is not allowed.
// plot(close[1] == na ? close : close[1])
// CORRECT
// Use the `na()` function to test for `na`.
plot(na(close[1]) ? close : close[1])
// CORRECT ALTERNATIVE
// `nz()` tests `close[1]` for `na`. It returns `close[1]` if it is not `na`, and `close` if it is.
plot(nz(close[1], close))
```

**REMARKS**

Do not use this variable with comparison operators to test values for na, as it might lead to unexpected behavior. Instead, use the na function. Note that na can be used to initialize variables when the initialization statement also specifies the variable's type.

**SEE ALSO**

na, nz, fixnan

---

### ohlc4

Is a shortcut for (open + high + low + close)/4

**TYPE**

series float

**SEE ALSO**

open, high, low, close, volume, time, hl2, hlc3, hlcc4

---

### open

Current open price.

**TYPE**

series float

**REMARKS**

Previous values may be accessed with square brackets operator [], e.g. open[1], open[2].

**SEE ALSO**

high, low, close, volume, time, hl2, hlc3, hlcc4, ohlc4, ask, bid

---

### polyline.all

Returns an array containing all current polyline instances drawn by the script.

**TYPE**

array<polyline>

**REMARKS**

The array is read-only. Index zero of the array references the ID of the oldest polyline object on the chart.

---

### second

Current bar second in exchange timezone.

**TYPE**

series int

**SEE ALSO**

second, time, year, month, weekofyear, dayofmonth, dayofweek, hour, minute

---

### session.isfirstbar

Returns true if the current bar is the first bar of the day's session, false otherwise. If extended session information is used, only returns true on the first bar of the pre-market bars.

**TYPE**

series bool

**EXAMPLE**

```pine
//@version=6
strategy("`session.isfirstbar` Example", overlay = true)
longCondition = year >= 2022
// Place a long order at the `close` of the trading session's first bar.
if session.isfirstbar and longCondition
    strategy.entry("Long", strategy.long)

// Close the long position at the `close` of the trading session's last bar.
if session.islastbar and barstate.isconfirmed
    strategy.close("Long", immediately = true)
```

**SEE ALSO**

session.isfirstbar_regular, session.islastbar, session.islastbar_regular

---

### session.isfirstbar_regular

Returns true on the first regular session bar of the day, false otherwise. The result is the same whether extended session information is used or not.

**TYPE**

series bool

**EXAMPLE**

```pine
//@version=6
strategy("`session.isfirstbar_regular` Example", overlay = true)
longCondition = year >= 2022
// Place a long order at the `close` of the trading session's first bar.
if session.isfirstbar and longCondition
    strategy.entry("Long", strategy.long)
// Close the long position at the `close` of the trading session's last bar.
if session.islastbar_regular and barstate.isconfirmed
    strategy.close("Long", immediately = true)
```

**SEE ALSO**

session.isfirstbar, session.islastbar

---

### session.islastbar

Returns true if the current bar is the last bar of the day's session, false otherwise. If extended session information is used, only returns true on the last bar of the post-market bars.

**TYPE**

series bool

**EXAMPLE**

```pine
//@version=6
strategy("`session.islastbar` Example", overlay = true)
longCondition = year >= 2022
// Place a long order at the `close` of the trading session's last bar.
// The position will enter on the `open` of next session's first bar.
if session.islastbar and longCondition
    strategy.entry("Long", strategy.long)
 // Close 'Long' position at the close of the last bar of the trading session
if session.islastbar and barstate.isconfirmed
    strategy.close("Long", immediately = true)
```

**REMARKS**

This variable is not guaranteed to return true once in every session because the last bar of the session might not exist if no trades occur during what should be the session's last bar.

This variable is not guaranteed to work as expected on non-standard chart types, e.g., Renko.

**SEE ALSO**

session.isfirstbar, session.islastbar_regular

---

### session.islastbar_regular

Returns true on the last regular session bar of the day, false otherwise. The result is the same whether extended session information is used or not.

**TYPE**

series bool

**EXAMPLE**

```pine
//@version=6
strategy("`session.islastbar_regular` Example", overlay = true)
longCondition = year >= 2022
// Place a long order at the `close` of the trading session's first bar.
if session.isfirstbar and longCondition
    strategy.entry("Long", strategy.long)
// Close the long position at the `close` of the trading session's last bar.
if session.islastbar_regular and barstate.isconfirmed
    strategy.close("Long", immediately = true)
```

**REMARKS**

This variable is not guaranteed to return true once in every session because the last bar of the session might not exist if no trades occur during what should be the session's last bar.

This variable is not guaranteed to work as expected on non-standard chart types, e.g., Renko.

**SEE ALSO**

session.isfirstbar, session.islastbar, session.isfirstbar_regular

---

### session.ismarket

Returns true if the current bar is a part of the regular trading hours (i.e. market hours), false otherwise.

**TYPE**

series bool

**SEE ALSO**

session.ispremarket, session.ispostmarket

---

### session.ispostmarket

Returns true if the current bar is a part of the post-market, false otherwise. On non-intraday charts always returns false.

**TYPE**

series bool

**SEE ALSO**

session.ismarket, session.ispremarket

---

### session.ispremarket

Returns true if the current bar is a part of the pre-market, false otherwise. On non-intraday charts always returns false.

**TYPE**

series bool

**SEE ALSO**

session.ismarket, session.ispostmarket

---

### strategy.account_currency

Returns the currency used to calculate results, which can be set in the strategy's properties.

**TYPE**

simple string

**SEE ALSO**

strategy, strategy.convert_to_account, strategy.convert_to_symbol

---

### strategy.avg_losing_trade

Returns the average amount of money lost per losing trade. Calculated as the sum of losses divided by the number of losing trades.

**TYPE**

series float

**SEE ALSO**

strategy.avg_losing_trade_percent

---

### strategy.avg_losing_trade_percent

Returns the average percentage loss per losing trade. Calculated as the sum of loss percentages divided by the number of losing trades.

**TYPE**

series float

**SEE ALSO**

strategy.avg_losing_trade

---

### strategy.avg_trade

Returns the average amount of money gained or lost per trade. Calculated as the sum of all profits and losses divided by the number of closed trades.

**TYPE**

series float

**SEE ALSO**

strategy.avg_trade_percent

---

### strategy.avg_trade_percent

Returns the average percentage gain or loss per trade. Calculated as the sum of all profit and loss percentages divided by the number of closed trades.

**TYPE**

series float

**SEE ALSO**

strategy.avg_trade

---

### strategy.avg_winning_trade

Returns the average amount of money gained per winning trade. Calculated as the sum of profits divided by the number of winning trades.

**TYPE**

series float

**SEE ALSO**

strategy.avg_winning_trade_percent

---

### strategy.avg_winning_trade_percent

Returns the average percentage gain per winning trade. Calculated as the sum of profit percentages divided by the number of winning trades.

**TYPE**

series float

**SEE ALSO**

strategy.avg_winning_trade

---

### strategy.closedtrades

Number of trades, which were closed for the whole trading range.

**TYPE**

series int

**SEE ALSO**

strategy.position_size, strategy.opentrades, strategy.wintrades, strategy.losstrades, strategy.eventrades

---

### strategy.closedtrades.first_index

The index, or trade number, of the first (oldest) trade listed in the List of Trades. This number is usually zero. If more trades than the allowed limit have been closed, the oldest trades are removed, and this number is the index of the oldest remaining trade.

**TYPE**

series int

**SEE ALSO**

strategy.position_size, strategy.opentrades, strategy.wintrades, strategy.losstrades, strategy.eventrades

---

### strategy.equity

Current equity (strategy.initial_capital + strategy.netprofit + strategy.openprofit).

**TYPE**

series float

**SEE ALSO**

strategy.netprofit, strategy.openprofit, strategy.position_size

---

### strategy.eventrades

Number of breakeven trades for the whole trading range.

**TYPE**

series int

**SEE ALSO**

strategy.position_size, strategy.opentrades, strategy.closedtrades, strategy.wintrades, strategy.losstrades

---

### strategy.grossloss

Total currency value of all completed losing trades.

**TYPE**

series float

**SEE ALSO**

strategy.netprofit, strategy.grossprofit

---

### strategy.grossloss_percent

The total value of all completed losing trades, expressed as a percentage of the initial capital.

**TYPE**

series float

**SEE ALSO**

strategy.grossloss

---

### strategy.grossprofit

Total currency value of all completed winning trades.

**TYPE**

series float

**SEE ALSO**

strategy.netprofit, strategy.grossloss

---

### strategy.grossprofit_percent

The total currency value of all completed winning trades, expressed as a percentage of the initial capital.

**TYPE**

series float

**SEE ALSO**

strategy.grossprofit

---

### strategy.initial_capital

The amount of initial capital set in the strategy properties.

**TYPE**

series float

**SEE ALSO**

strategy

---

### strategy.losstrades

Number of unprofitable trades for the whole trading range.

**TYPE**

series int

**SEE ALSO**

strategy.position_size, strategy.opentrades, strategy.closedtrades, strategy.wintrades, strategy.eventrades

---

### strategy.margin_liquidation_price

When margin is used in a strategy, returns the price point where a simulated margin call will occur and liquidate enough of the position to meet the margin requirements.

**TYPE**

series float

**EXAMPLE**

```pine
//@version=6
strategy("Margin call management", overlay = true, margin_long = 25, margin_short = 25,
  default_qty_type = strategy.percent_of_equity, default_qty_value = 395)

float maFast = ta.sma(close, 14)
float maSlow = ta.sma(close, 28)

if ta.crossover(maFast, maSlow)
    strategy.entry("Long", strategy.long)

if ta.crossunder(maFast, maSlow)
    strategy.entry("Short", strategy.short)

changePercent(v1, v2) =>
    float result = (v1 - v2) * 100 / math.abs(v2)

// exit when we're 10% away from a margin call, to prevent it.
if math.abs(changePercent(close, strategy.margin_liquidation_price)) <= 10
    strategy.close("Long")
    strategy.close("Short")
```

**REMARKS**

The variable returns na if the strategy does not use margin, i.e., the strategy declaration statement does not specify an argument for the margin_long or margin_short parameter.

---

### strategy.max_contracts_held_all

Maximum number of contracts/shares/lots/units in one trade for the whole trading range.

**TYPE**

series float

**SEE ALSO**

strategy.position_size, strategy.max_contracts_held_long, strategy.max_contracts_held_short

---

### strategy.max_contracts_held_long

Maximum number of contracts/shares/lots/units in one long trade for the whole trading range.

**TYPE**

series float

**SEE ALSO**

strategy.position_size, strategy.max_contracts_held_all, strategy.max_contracts_held_short

---

### strategy.max_contracts_held_short

Maximum number of contracts/shares/lots/units in one short trade for the whole trading range.

**TYPE**

series float

**SEE ALSO**

strategy.position_size, strategy.max_contracts_held_all, strategy.max_contracts_held_long

---

### strategy.max_drawdown

Maximum equity drawdown value for the whole trading range.

**TYPE**

series float

**SEE ALSO**

strategy.netprofit, strategy.equity, strategy.max_runup

---

### strategy.max_drawdown_percent

The maximum equity drawdown value for the whole trading range, expressed as a percentage and calculated by formula: Lowest Value During Trade / (Entry Price x Quantity) * 100.

**TYPE**

series float

**SEE ALSO**

strategy.max_drawdown

---

### strategy.max_runup

Maximum equity run-up value for the whole trading range.

**TYPE**

series float

**SEE ALSO**

strategy.netprofit, strategy.equity, strategy.max_drawdown

---

### strategy.max_runup_percent

The maximum equity run-up value for the whole trading range, expressed as a percentage and calculated by formula: Highest Value During Trade / (Entry Price x Quantity) * 100.

**TYPE**

series float

**SEE ALSO**

strategy.max_runup

---

### strategy.netprofit

Total currency value of all completed trades.

**TYPE**

series float

**SEE ALSO**

strategy.openprofit, strategy.position_size, strategy.grossprofit, strategy.grossloss

---

### strategy.netprofit_percent

The total value of all completed trades, expressed as a percentage of the initial capital.

**TYPE**

series float

**SEE ALSO**

strategy.netprofit

---

### strategy.openprofit

Current unrealized profit or loss for all open positions.

**TYPE**

series float

**SEE ALSO**

strategy.netprofit, strategy.position_size

---

### strategy.openprofit_percent

The current unrealized profit or loss for all open positions, expressed as a percentage and calculated by formula: openPL / realizedEquity * 100.

**TYPE**

series float

**SEE ALSO**

strategy.openprofit

---

### strategy.opentrades

Number of market position entries, which were not closed and remain opened. If there is no open market position, 0 is returned.

**TYPE**

series int

**SEE ALSO**

strategy.position_size

---

### strategy.opentrades.capital_held

Returns the capital amount currently held by open trades.

**TYPE**

series float

**EXAMPLE**

```pine
//@version=6
strategy(
   "strategy.opentrades.capital_held example", overlay=false, margin_long=50, margin_short=50,
   default_qty_type = strategy.percent_of_equity, default_qty_value = 100
 )

// Enter a short position on the first bar.
if barstate.isfirst
    strategy.entry("Short", strategy.short)

// Plot the capital held by the short position.
plot(strategy.opentrades.capital_held, "Capital held")
// Highlight the chart background if the position is completely closed by margin calls.
bgcolor(bar_index > 0 and strategy.opentrades.capital_held == 0 ? color.new(color.red, 60) : na)
```

**REMARKS**

This variable returns na if the strategy does not simulate funding trades with a portion of the hypothetical account, i.e., if the strategy function does not include nonzero margin_long or margin_short arguments.

---

### strategy.position_avg_price

Average entry price of current market position. If the market position is flat, 'NaN' is returned.

**TYPE**

series float

**SEE ALSO**

strategy.position_size

---

### strategy.position_entry_name

Name of the order that initially opened current market position.

**TYPE**

series string

**SEE ALSO**

strategy.position_size

---

### strategy.position_size

Direction and size of the current market position. If the value is > 0, the market position is long. If the value is < 0, the market position is short. The absolute value is the number of contracts/shares/lots/units in trade (position size).

**TYPE**

series float

**SEE ALSO**

strategy.position_avg_price

---

### strategy.wintrades

Number of profitable trades for the whole trading range.

**TYPE**

series int

**SEE ALSO**

strategy.position_size, strategy.opentrades, strategy.closedtrades, strategy.losstrades, strategy.eventrades

---

### syminfo.basecurrency

Returns a string containing the code representing the symbol's base currency (i.e., the traded currency or coin) if the instrument is a Forex or Crypto pair or a derivative based on such a pair. Otherwise, it returns an empty string. For example, this variable returns "EUR" for "EURJPY", "BTC" for "BTCUSDT", "CAD" for "CME:6C1!", and "" for "NASDAQ:AAPL".

**TYPE**

simple string

**SEE ALSO**

syminfo.currency, syminfo.ticker

---

### syminfo.country

Returns the two-letter code of the country where the symbol is traded, in the ISO 3166-1 alpha-2 format, or na if the exchange is not directly tied to a specific country. For example, on "NASDAQ:AAPL" it will return "US", on "LSE:AAPL" it will return "GB", and on "BITSTAMP:BTCUSD it will return na.

**TYPE**

simple string

---

### syminfo.currency

Returns a string containing the code representing the currency of the symbol's prices. For example, this variable returns "USD" for "NASDAQ:AAPL" and "JPY" for "EURJPY".

**TYPE**

simple string

**SEE ALSO**

syminfo.basecurrency, syminfo.ticker, currency.USD, currency.EUR

---

### syminfo.current_contract

The ticker identifier of the underlying contract, if the current symbol is a continuous futures contract; na otherwise.

**TYPE**

simple string

**SEE ALSO**

syminfo.ticker, syminfo.description

---

### syminfo.description

Description for the current symbol.

**TYPE**

simple string

**SEE ALSO**

syminfo.ticker, syminfo.prefix

---

### syminfo.employees

The number of employees the company has.

**TYPE**

simple int

**EXAMPLE**

```pine
//@version=6
indicator("syminfo simple")
//@variable A table containing information about a company's employees, shareholders, and shares.
var result_table = table.new(position = position.top_right, columns = 2, rows = 5, border_width = 1)
if barstate.islastconfirmedhistory
    // Add header cells
    table.cell(table_id = result_table, column = 0, row = 0, text = "name")
    table.cell(table_id = result_table, column = 1, row = 0, text = "value")
    // Add employee info cells.
    table.cell(table_id = result_table, column = 0, row = 1, text = "employees")
    table.cell(table_id = result_table, column = 1, row = 1, text = str.tostring(syminfo.employees))
    // Add shareholder cells.
    table.cell(table_id = result_table, column = 0, row = 2, text = "shareholders")
    table.cell(table_id = result_table, column = 1, row = 2, text = str.tostring(syminfo.shareholders))
    // Add float shares outstanding cells.
    table.cell(table_id = result_table, column = 0, row = 3, text = "shares_outstanding_float")
    table.cell(table_id = result_table, column = 1, row = 3, text = str.tostring(syminfo.shares_outstanding_float))
    // Add total shares outstanding cells.
    table.cell(table_id = result_table, column = 0, row = 4, text = "shares_outstanding_total")
    table.cell(table_id = result_table, column = 1, row = 4, text = str.tostring(syminfo.shares_outstanding_total))
```

**SEE ALSO**

syminfo.shareholders, syminfo.shares_outstanding_float, syminfo.shares_outstanding_total

---

### syminfo.expiration_date

A UNIX timestamp representing the start of the last day of the current futures contract. This variable is only compatible with non-continuous futures symbols. On other symbols, it returns na.

**TYPE**

simple int

---

### syminfo.industry

Returns the industry of the symbol, or na if the symbol has no industry. Example: "Internet Software/Services", "Packaged software", "Integrated Oil", "Motor Vehicles", etc. These are the same values one can see in the chart's "Symbol info" window.

**TYPE**

simple string

**REMARKS**

A sector is a broad section of the economy. An industry is a narrower classification. NASDAQ:CAT (Caterpillar, Inc.) for example, belongs to the "Producer Manufacturing" sector and the "Trucks/Construction/Farm Machinery" industry.

---

### syminfo.main_tickerid

A ticker identifier representing the current chart's symbol. The value contains an exchange prefix and a symbol name, separated by a colon (e.g., "NASDAQ:AAPL"). It can also include information about data modifications such as dividend adjustment, non-standard chart type, currency conversion, etc. Unlike syminfo.tickerid, this variable's value does not change when used in the expression argument of a request.*() function call.

**TYPE**

simple string

**SEE ALSO**

ticker.new, timeframe.main_period, syminfo.tickerid, syminfo.ticker, timeframe.period, timeframe.multiplier, syminfo.root

---

### syminfo.mincontract

The smallest amount of the current symbol that can be traded. This limit is set by the exchange. For cryptocurrencies, it is often less than 1 token. For most other types of asset, it is often 1.

**TYPE**

simple float

**SEE ALSO**

syminfo.mintick, syminfo.pointvalue

---

### syminfo.minmove

Returns a whole number used to calculate the smallest increment between a symbol's price movements (syminfo.mintick). It is the numerator in the syminfo.mintick formula: syminfo.minmove / syminfo.pricescale = syminfo.mintick.

**TYPE**

simple int

**SEE ALSO**

ticker.new, syminfo.ticker, timeframe.period, timeframe.multiplier, syminfo.root

---

### syminfo.mintick

Min tick value for the current symbol.

**TYPE**

simple float

**SEE ALSO**

syminfo.pointvalue, syminfo.mincontract

---

### syminfo.pointvalue

The chart price of a security multiplied by the point value equals the actual price of the traded security.

For all types of security except futures, the point value is usually equal to 1 and can therefore be ignored. For futures, the prices shown on the chart are either the cost of a single futures contract, in which case the point value is 1, or the price of a single unit of the underlying commodity, in which case the point value represents the number of units included in a single contract.

For example, the price of the "COMEX:GC1!" gold futures chart reflects the price of a single troy ounce of gold. However, a single GC futures contract comprises 100 troy ounces, as defined by the COMEX exchange. So when the price on the "GC1!" chart is 2000 USD, a single contract costs 2000 USD * 100 troy ounces = 200,000 USD. This calculation is important in backtesting, because the strategy engine takes the point value into account, and does not open a position if there is not enough capital.

The point value is also displayed in the Security Info window for a given asset.

**TYPE**

simple float

**SEE ALSO**

syminfo.mintick, syminfo.mincontract

---

### syminfo.prefix

Prefix of current symbol name (i.e. for 'CME_EOD:TICKER' prefix is 'CME_EOD').

**TYPE**

simple string

**EXAMPLE**

```pine
//@version=6
indicator("syminfo.prefix")

// If current chart symbol is 'BATS:MSFT' then syminfo.prefix is 'BATS'.
if barstate.islastconfirmedhistory
    label.new(bar_index, high, text=syminfo.prefix)
```

**SEE ALSO**

syminfo.ticker, syminfo.tickerid

---

### syminfo.pricescale

Returns a whole number used to calculate the smallest increment between a symbol's price movements (syminfo.mintick). It is the denominator in the syminfo.mintick formula: syminfo.minmove / syminfo.pricescale = syminfo.mintick.

**TYPE**

simple int

**SEE ALSO**

ticker.new, syminfo.ticker, timeframe.period, timeframe.multiplier, syminfo.root

---

### syminfo.recommendations_buy

The number of analysts who gave the current symbol a "Buy" rating.

**TYPE**

series int

**EXAMPLE**

```pine
//@version=6
indicator("syminfo recommendations", overlay = true)
//@variable A table containing information about analyst recommendations.
var table ratings = table.new(position.top_right, 8, 2, frame_color = #000000)
if barstate.islastconfirmedhistory
    //@variable The time value one year from the date of the last analyst recommendations.
    int YTD = syminfo.target_price_date + timeframe.in_seconds("12M") * 1000
    // Add header cells.
    table.cell(ratings, 0, 0, "Start Date", bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 1, 0, "End Date", bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 2, 0, "Buy", bgcolor = color.teal, text_color = #000000, text_size = size.large)
    table.cell(ratings, 3, 0, "Strong Buy", bgcolor = color.lime, text_color = #000000, text_size = size.large)
    table.cell(ratings, 4, 0, "Sell", bgcolor = color.maroon, text_color = #000000, text_size = size.large)
    table.cell(ratings, 5, 0, "Strong Sell", bgcolor = color.red, text_color = #000000, text_size = size.large)
    table.cell(ratings, 6, 0, "Hold", bgcolor = color.orange, text_color = #000000, text_size = size.large)
    table.cell(ratings, 7, 0, "Total", bgcolor = color.silver, text_color = #000000, text_size = size.large)
    // Recommendation strings
    string startDate         = str.format_time(syminfo.recommendations_date, "yyyy-MM-dd")
    string endDate           = str.format_time(YTD, "yyyy-MM-dd")
    string buyRatings        = str.tostring(syminfo.recommendations_buy)
    string strongBuyRatings  = str.tostring(syminfo.recommendations_buy_strong)
    string sellRatings       = str.tostring(syminfo.recommendations_sell)
    string strongSellRatings = str.tostring(syminfo.recommendations_sell_strong)
    string holdRatings       = str.tostring(syminfo.recommendations_hold)
    string totalRatings      = str.tostring(syminfo.recommendations_total)
    // Add value cells
    table.cell(ratings, 0, 1, startDate, bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 1, 1, endDate, bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 2, 1, buyRatings, bgcolor = color.teal, text_color = #000000, text_size = size.large)
    table.cell(ratings, 3, 1, strongBuyRatings, bgcolor = color.lime, text_color = #000000, text_size = size.large)
    table.cell(ratings, 4, 1, sellRatings, bgcolor = color.maroon, text_color = #000000, text_size = size.large)
```

**SEE ALSO**

syminfo.recommendations_buy_strong, syminfo.recommendations_date, syminfo.recommendations_hold, syminfo.recommendations_total, syminfo.recommendations_sell, syminfo.recommendations_sell_strong

---

### syminfo.recommendations_buy_strong

The number of analysts who gave the current symbol a "Strong Buy" rating.

**TYPE**

series int

**EXAMPLE**

```pine
//@version=6
indicator("syminfo recommendations", overlay = true)
//@variable A table containing information about analyst recommendations.
var table ratings = table.new(position.top_right, 8, 2, frame_color = #000000)
if barstate.islastconfirmedhistory
    //@variable The time value one year from the date of the last analyst recommendations.
    int YTD = syminfo.target_price_date + timeframe.in_seconds("12M") * 1000
    // Add header cells.
    table.cell(ratings, 0, 0, "Start Date", bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 1, 0, "End Date", bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 2, 0, "Buy", bgcolor = color.teal, text_color = #000000, text_size = size.large)
    table.cell(ratings, 3, 0, "Strong Buy", bgcolor = color.lime, text_color = #000000, text_size = size.large)
    table.cell(ratings, 4, 0, "Sell", bgcolor = color.maroon, text_color = #000000, text_size = size.large)
    table.cell(ratings, 5, 0, "Strong Sell", bgcolor = color.red, text_color = #000000, text_size = size.large)
    table.cell(ratings, 6, 0, "Hold", bgcolor = color.orange, text_color = #000000, text_size = size.large)
    table.cell(ratings, 7, 0, "Total", bgcolor = color.silver, text_color = #000000, text_size = size.large)
    // Recommendation strings
    string startDate         = str.format_time(syminfo.recommendations_date, "yyyy-MM-dd")
    string endDate           = str.format_time(YTD, "yyyy-MM-dd")
    string buyRatings        = str.tostring(syminfo.recommendations_buy)
    string strongBuyRatings  = str.tostring(syminfo.recommendations_buy_strong)
    string sellRatings       = str.tostring(syminfo.recommendations_sell)
    string strongSellRatings = str.tostring(syminfo.recommendations_sell_strong)
    string holdRatings       = str.tostring(syminfo.recommendations_hold)
    string totalRatings      = str.tostring(syminfo.recommendations_total)
    // Add value cells
    table.cell(ratings, 0, 1, startDate, bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 1, 1, endDate, bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 2, 1, buyRatings, bgcolor = color.teal, text_color = #000000, text_size = size.large)
    table.cell(ratings, 3, 1, strongBuyRatings, bgcolor = color.lime, text_color = #000000, text_size = size.large)
    table.cell(ratings, 4, 1, sellRatings, bgcolor = color.maroon, text_color = #000000, text_size = size.large)
```

**SEE ALSO**

syminfo.recommendations_buy, syminfo.recommendations_date, syminfo.recommendations_hold, syminfo.recommendations_total, syminfo.recommendations_sell, syminfo.recommendations_sell_strong

---

### syminfo.recommendations_date

The starting date of the last set of recommendations for the current symbol.

**TYPE**

series int

**EXAMPLE**

```pine
//@version=6
indicator("syminfo recommendations", overlay = true)
//@variable A table containing information about analyst recommendations.
var table ratings = table.new(position.top_right, 8, 2, frame_color = #000000)
if barstate.islastconfirmedhistory
    //@variable The time value one year from the date of the last analyst recommendations.
    int YTD = syminfo.target_price_date + timeframe.in_seconds("12M") * 1000
    // Add header cells.
    table.cell(ratings, 0, 0, "Start Date", bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 1, 0, "End Date", bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 2, 0, "Buy", bgcolor = color.teal, text_color = #000000, text_size = size.large)
    table.cell(ratings, 3, 0, "Strong Buy", bgcolor = color.lime, text_color = #000000, text_size = size.large)
    table.cell(ratings, 4, 0, "Sell", bgcolor = color.maroon, text_color = #000000, text_size = size.large)
    table.cell(ratings, 5, 0, "Strong Sell", bgcolor = color.red, text_color = #000000, text_size = size.large)
    table.cell(ratings, 6, 0, "Hold", bgcolor = color.orange, text_color = #000000, text_size = size.large)
    table.cell(ratings, 7, 0, "Total", bgcolor = color.silver, text_color = #000000, text_size = size.large)
    // Recommendation strings
    string startDate         = str.format_time(syminfo.recommendations_date, "yyyy-MM-dd")
    string endDate           = str.format_time(YTD, "yyyy-MM-dd")
    string buyRatings        = str.tostring(syminfo.recommendations_buy)
    string strongBuyRatings  = str.tostring(syminfo.recommendations_buy_strong)
    string sellRatings       = str.tostring(syminfo.recommendations_sell)
    string strongSellRatings = str.tostring(syminfo.recommendations_sell_strong)
    string holdRatings       = str.tostring(syminfo.recommendations_hold)
    string totalRatings      = str.tostring(syminfo.recommendations_total)
    // Add value cells
    table.cell(ratings, 0, 1, startDate, bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 1, 1, endDate, bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 2, 1, buyRatings, bgcolor = color.teal, text_color = #000000, text_size = size.large)
    table.cell(ratings, 3, 1, strongBuyRatings, bgcolor = color.lime, text_color = #000000, text_size = size.large)
    table.cell(ratings, 4, 1, sellRatings, bgcolor = color.maroon, text_color = #000000, text_size = size.large)
```

**SEE ALSO**

syminfo.recommendations_buy, syminfo.recommendations_buy_strong, syminfo.recommendations_hold, syminfo.recommendations_total, syminfo.recommendations_sell, syminfo.recommendations_sell_strong

---

### syminfo.recommendations_hold

The number of analysts who gave the current symbol a "Hold" rating.

**TYPE**

series int

**EXAMPLE**

```pine
//@version=6
indicator("syminfo recommendations", overlay = true)
//@variable A table containing information about analyst recommendations.
var table ratings = table.new(position.top_right, 8, 2, frame_color = #000000)
if barstate.islastconfirmedhistory
    //@variable The time value one year from the date of the last analyst recommendations.
    int YTD = syminfo.target_price_date + timeframe.in_seconds("12M") * 1000
    // Add header cells.
    table.cell(ratings, 0, 0, "Start Date", bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 1, 0, "End Date", bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 2, 0, "Buy", bgcolor = color.teal, text_color = #000000, text_size = size.large)
    table.cell(ratings, 3, 0, "Strong Buy", bgcolor = color.lime, text_color = #000000, text_size = size.large)
    table.cell(ratings, 4, 0, "Sell", bgcolor = color.maroon, text_color = #000000, text_size = size.large)
    table.cell(ratings, 5, 0, "Strong Sell", bgcolor = color.red, text_color = #000000, text_size = size.large)
    table.cell(ratings, 6, 0, "Hold", bgcolor = color.orange, text_color = #000000, text_size = size.large)
    table.cell(ratings, 7, 0, "Total", bgcolor = color.silver, text_color = #000000, text_size = size.large)
    // Recommendation strings
    string startDate         = str.format_time(syminfo.recommendations_date, "yyyy-MM-dd")
    string endDate           = str.format_time(YTD, "yyyy-MM-dd")
    string buyRatings        = str.tostring(syminfo.recommendations_buy)
    string strongBuyRatings  = str.tostring(syminfo.recommendations_buy_strong)
    string sellRatings       = str.tostring(syminfo.recommendations_sell)
    string strongSellRatings = str.tostring(syminfo.recommendations_sell_strong)
    string holdRatings       = str.tostring(syminfo.recommendations_hold)
    string totalRatings      = str.tostring(syminfo.recommendations_total)
    // Add value cells
    table.cell(ratings, 0, 1, startDate, bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 1, 1, endDate, bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 2, 1, buyRatings, bgcolor = color.teal, text_color = #000000, text_size = size.large)
    table.cell(ratings, 3, 1, strongBuyRatings, bgcolor = color.lime, text_color = #000000, text_size = size.large)
    table.cell(ratings, 4, 1, sellRatings, bgcolor = color.maroon, text_color = #000000, text_size = size.large)
```

**SEE ALSO**

syminfo.recommendations_buy, syminfo.recommendations_buy_strong, syminfo.recommendations_date, syminfo.recommendations_total, syminfo.recommendations_sell, syminfo.recommendations_sell_strong

---

### syminfo.recommendations_sell

The number of analysts who gave the current symbol a "Sell" rating.

**TYPE**

series int

**EXAMPLE**

```pine
//@version=6
indicator("syminfo recommendations", overlay = true)
//@variable A table containing information about analyst recommendations.
var table ratings = table.new(position.top_right, 8, 2, frame_color = #000000)
if barstate.islastconfirmedhistory
    //@variable The time value one year from the date of the last analyst recommendations.
    int YTD = syminfo.target_price_date + timeframe.in_seconds("12M") * 1000
    // Add header cells.
    table.cell(ratings, 0, 0, "Start Date", bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 1, 0, "End Date", bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 2, 0, "Buy", bgcolor = color.teal, text_color = #000000, text_size = size.large)
    table.cell(ratings, 3, 0, "Strong Buy", bgcolor = color.lime, text_color = #000000, text_size = size.large)
    table.cell(ratings, 4, 0, "Sell", bgcolor = color.maroon, text_color = #000000, text_size = size.large)
    table.cell(ratings, 5, 0, "Strong Sell", bgcolor = color.red, text_color = #000000, text_size = size.large)
    table.cell(ratings, 6, 0, "Hold", bgcolor = color.orange, text_color = #000000, text_size = size.large)
    table.cell(ratings, 7, 0, "Total", bgcolor = color.silver, text_color = #000000, text_size = size.large)
    // Recommendation strings
    string startDate         = str.format_time(syminfo.recommendations_date, "yyyy-MM-dd")
    string endDate           = str.format_time(YTD, "yyyy-MM-dd")
    string buyRatings        = str.tostring(syminfo.recommendations_buy)
    string strongBuyRatings  = str.tostring(syminfo.recommendations_buy_strong)
    string sellRatings       = str.tostring(syminfo.recommendations_sell)
    string strongSellRatings = str.tostring(syminfo.recommendations_sell_strong)
    string holdRatings       = str.tostring(syminfo.recommendations_hold)
    string totalRatings      = str.tostring(syminfo.recommendations_total)
    // Add value cells
    table.cell(ratings, 0, 1, startDate, bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 1, 1, endDate, bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 2, 1, buyRatings, bgcolor = color.teal, text_color = #000000, text_size = size.large)
    table.cell(ratings, 3, 1, strongBuyRatings, bgcolor = color.lime, text_color = #000000, text_size = size.large)
    table.cell(ratings, 4, 1, sellRatings, bgcolor = color.maroon, text_color = #000000, text_size = size.large)
```

**SEE ALSO**

syminfo.recommendations_buy, syminfo.recommendations_buy_strong, syminfo.recommendations_date, syminfo.recommendations_hold, syminfo.recommendations_total, syminfo.recommendations_sell_strong

---

### syminfo.recommendations_sell_strong

The number of analysts who gave the current symbol a "Strong Sell" rating.

**TYPE**

series int

**EXAMPLE**

```pine
//@version=6
indicator("syminfo recommendations", overlay = true)
//@variable A table containing information about analyst recommendations.
var table ratings = table.new(position.top_right, 8, 2, frame_color = #000000)
if barstate.islastconfirmedhistory
    //@variable The time value one year from the date of the last analyst recommendations.
    int YTD = syminfo.target_price_date + timeframe.in_seconds("12M") * 1000
    // Add header cells.
    table.cell(ratings, 0, 0, "Start Date", bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 1, 0, "End Date", bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 2, 0, "Buy", bgcolor = color.teal, text_color = #000000, text_size = size.large)
    table.cell(ratings, 3, 0, "Strong Buy", bgcolor = color.lime, text_color = #000000, text_size = size.large)
    table.cell(ratings, 4, 0, "Sell", bgcolor = color.maroon, text_color = #000000, text_size = size.large)
    table.cell(ratings, 5, 0, "Strong Sell", bgcolor = color.red, text_color = #000000, text_size = size.large)
    table.cell(ratings, 6, 0, "Hold", bgcolor = color.orange, text_color = #000000, text_size = size.large)
    table.cell(ratings, 7, 0, "Total", bgcolor = color.silver, text_color = #000000, text_size = size.large)
    // Recommendation strings
    string startDate         = str.format_time(syminfo.recommendations_date, "yyyy-MM-dd")
    string endDate           = str.format_time(YTD, "yyyy-MM-dd")
    string buyRatings        = str.tostring(syminfo.recommendations_buy)
    string strongBuyRatings  = str.tostring(syminfo.recommendations_buy_strong)
    string sellRatings       = str.tostring(syminfo.recommendations_sell)
    string strongSellRatings = str.tostring(syminfo.recommendations_sell_strong)
    string holdRatings       = str.tostring(syminfo.recommendations_hold)
    string totalRatings      = str.tostring(syminfo.recommendations_total)
    // Add value cells
    table.cell(ratings, 0, 1, startDate, bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 1, 1, endDate, bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 2, 1, buyRatings, bgcolor = color.teal, text_color = #000000, text_size = size.large)
    table.cell(ratings, 3, 1, strongBuyRatings, bgcolor = color.lime, text_color = #000000, text_size = size.large)
    table.cell(ratings, 4, 1, sellRatings, bgcolor = color.maroon, text_color = #000000, text_size = size.large)
```

**SEE ALSO**

syminfo.recommendations_buy, syminfo.recommendations_buy_strong, syminfo.recommendations_date, syminfo.recommendations_hold, syminfo.recommendations_total, syminfo.recommendations_sell

---

### syminfo.recommendations_total

The total number of recommendations for the current symbol.

**TYPE**

series int

**EXAMPLE**

```pine
//@version=6
indicator("syminfo recommendations", overlay = true)
//@variable A table containing information about analyst recommendations.
var table ratings = table.new(position.top_right, 8, 2, frame_color = #000000)
if barstate.islastconfirmedhistory
    //@variable The time value one year from the date of the last analyst recommendations.
    int YTD = syminfo.target_price_date + timeframe.in_seconds("12M") * 1000
    // Add header cells.
    table.cell(ratings, 0, 0, "Start Date", bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 1, 0, "End Date", bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 2, 0, "Buy", bgcolor = color.teal, text_color = #000000, text_size = size.large)
    table.cell(ratings, 3, 0, "Strong Buy", bgcolor = color.lime, text_color = #000000, text_size = size.large)
    table.cell(ratings, 4, 0, "Sell", bgcolor = color.maroon, text_color = #000000, text_size = size.large)
    table.cell(ratings, 5, 0, "Strong Sell", bgcolor = color.red, text_color = #000000, text_size = size.large)
    table.cell(ratings, 6, 0, "Hold", bgcolor = color.orange, text_color = #000000, text_size = size.large)
    table.cell(ratings, 7, 0, "Total", bgcolor = color.silver, text_color = #000000, text_size = size.large)
    // Recommendation strings
    string startDate         = str.format_time(syminfo.recommendations_date, "yyyy-MM-dd")
    string endDate           = str.format_time(YTD, "yyyy-MM-dd")
    string buyRatings        = str.tostring(syminfo.recommendations_buy)
    string strongBuyRatings  = str.tostring(syminfo.recommendations_buy_strong)
    string sellRatings       = str.tostring(syminfo.recommendations_sell)
    string strongSellRatings = str.tostring(syminfo.recommendations_sell_strong)
    string holdRatings       = str.tostring(syminfo.recommendations_hold)
    string totalRatings      = str.tostring(syminfo.recommendations_total)
    // Add value cells
    table.cell(ratings, 0, 1, startDate, bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 1, 1, endDate, bgcolor = color.gray, text_color = #000000, text_size = size.large)
    table.cell(ratings, 2, 1, buyRatings, bgcolor = color.teal, text_color = #000000, text_size = size.large)
    table.cell(ratings, 3, 1, strongBuyRatings, bgcolor = color.lime, text_color = #000000, text_size = size.large)
    table.cell(ratings, 4, 1, sellRatings, bgcolor = color.maroon, text_color = #000000, text_size = size.large)
```

**SEE ALSO**

syminfo.recommendations_buy, syminfo.recommendations_buy_strong, syminfo.recommendations_date, syminfo.recommendations_hold, syminfo.recommendations_sell, syminfo.recommendations_sell_strong

---

### syminfo.root

Root for derivatives like futures contract. For other symbols returns the same value as syminfo.ticker.

**TYPE**

simple string

**EXAMPLE**

```pine
//@version=6
indicator("syminfo.root")

// If the current chart symbol is continuous futures ('ES1!'), it would display 'ES'.
if barstate.islastconfirmedhistory
    label.new(bar_index, high, syminfo.root)
```

**SEE ALSO**

syminfo.ticker, syminfo.tickerid

---

### syminfo.sector

Returns the sector of the symbol, or na if the symbol has no sector. Example: "Electronic Technology", "Technology services", "Energy Minerals", "Consumer Durables", etc. These are the same values one can see in the chart's "Symbol info" window.

**TYPE**

simple string

**REMARKS**

A sector is a broad section of the economy. An industry is a narrower classification. NASDAQ:CAT (Caterpillar, Inc.) for example, belongs to the "Producer Manufacturing" sector and the "Trucks/Construction/Farm Machinery" industry.

---

### syminfo.session

Session type of the chart main series. Possible values are session.regular, session.extended.

**TYPE**

simple string

**SEE ALSO**

session.regular, session.extended

---

### syminfo.shareholders

The number of shareholders the company has.

**TYPE**

simple int

**EXAMPLE**

```pine
//@version=6
indicator("syminfo simple")
//@variable A table containing information about a company's employees, shareholders, and shares.
var result_table = table.new(position = position.top_right, columns = 2, rows = 5, border_width = 1)
if barstate.islastconfirmedhistory
    // Add header cells
    table.cell(table_id = result_table, column = 0, row = 0, text = "name")
    table.cell(table_id = result_table, column = 1, row = 0, text = "value")
    // Add employee info cells.
    table.cell(table_id = result_table, column = 0, row = 1, text = "employees")
    table.cell(table_id = result_table, column = 1, row = 1, text = str.tostring(syminfo.employees))
    // Add shareholder cells.
    table.cell(table_id = result_table, column = 0, row = 2, text = "shareholders")
    table.cell(table_id = result_table, column = 1, row = 2, text = str.tostring(syminfo.shareholders))
    // Add float shares outstanding cells.
    table.cell(table_id = result_table, column = 0, row = 3, text = "shares_outstanding_float")
    table.cell(table_id = result_table, column = 1, row = 3, text = str.tostring(syminfo.shares_outstanding_float))
    // Add total shares outstanding cells.
    table.cell(table_id = result_table, column = 0, row = 4, text = "shares_outstanding_total")
    table.cell(table_id = result_table, column = 1, row = 4, text = str.tostring(syminfo.shares_outstanding_total))
```

**SEE ALSO**

syminfo.employees, syminfo.shares_outstanding_float, syminfo.shares_outstanding_total

---

### syminfo.shares_outstanding_float

The total number of shares outstanding a company has available, excluding any of its restricted shares.

**TYPE**

simple float

**EXAMPLE**

```pine
//@version=6
indicator("syminfo simple")
//@variable A table containing information about a company's employees, shareholders, and shares.
var result_table = table.new(position = position.top_right, columns = 2, rows = 5, border_width = 1)
if barstate.islastconfirmedhistory
    // Add header cells
    table.cell(table_id = result_table, column = 0, row = 0, text = "name")
    table.cell(table_id = result_table, column = 1, row = 0, text = "value")
    // Add employee info cells.
    table.cell(table_id = result_table, column = 0, row = 1, text = "employees")
    table.cell(table_id = result_table, column = 1, row = 1, text = str.tostring(syminfo.employees))
    // Add shareholder cells.
    table.cell(table_id = result_table, column = 0, row = 2, text = "shareholders")
    table.cell(table_id = result_table, column = 1, row = 2, text = str.tostring(syminfo.shareholders))
    // Add float shares outstanding cells.
    table.cell(table_id = result_table, column = 0, row = 3, text = "shares_outstanding_float")
    table.cell(table_id = result_table, column = 1, row = 3, text = str.tostring(syminfo.shares_outstanding_float))
    // Add total shares outstanding cells.
    table.cell(table_id = result_table, column = 0, row = 4, text = "shares_outstanding_total")
    table.cell(table_id = result_table, column = 1, row = 4, text = str.tostring(syminfo.shares_outstanding_total))
```

**SEE ALSO**

syminfo.employees, syminfo.shareholders, syminfo.shares_outstanding_total

---

### syminfo.shares_outstanding_total

The total number of shares outstanding a company has available, including restricted shares held by insiders, major shareholders, and employees.

**TYPE**

simple int

**EXAMPLE**

```pine
//@version=6
indicator("syminfo simple")
//@variable A table containing information about a company's employees, shareholders, and shares.
var result_table = table.new(position = position.top_right, columns = 2, rows = 5, border_width = 1)
if barstate.islastconfirmedhistory
    // Add header cells
    table.cell(table_id = result_table, column = 0, row = 0, text = "name")
    table.cell(table_id = result_table, column = 1, row = 0, text = "value")
    // Add employee info cells.
    table.cell(table_id = result_table, column = 0, row = 1, text = "employees")
    table.cell(table_id = result_table, column = 1, row = 1, text = str.tostring(syminfo.employees))
    // Add shareholder cells.
    table.cell(table_id = result_table, column = 0, row = 2, text = "shareholders")
    table.cell(table_id = result_table, column = 1, row = 2, text = str.tostring(syminfo.shareholders))
    // Add float shares outstanding cells.
    table.cell(table_id = result_table, column = 0, row = 3, text = "shares_outstanding_float")
    table.cell(table_id = result_table, column = 1, row = 3, text = str.tostring(syminfo.shares_outstanding_float))
    // Add total shares outstanding cells.
    table.cell(table_id = result_table, column = 0, row = 4, text = "shares_outstanding_total")
    table.cell(table_id = result_table, column = 1, row = 4, text = str.tostring(syminfo.shares_outstanding_total))
```

**SEE ALSO**

syminfo.employees, syminfo.shareholders, syminfo.shares_outstanding_float

---

### syminfo.target_price_average

The average of the last yearly price targets for the symbol predicted by analysts.

**TYPE**

series float

**EXAMPLE**

```pine
//@version=6
indicator("syminfo target_price")
if barstate.islastconfirmedhistory
    //@variable The time value one year from the date of the last analyst recommendations.
    int YTD = syminfo.target_price_date + timeframe.in_seconds("12M") * 1000
    //@variable A line connecting the current `close` to the highest yearly price estimate.
    highLine = line.new(time, close, YTD, syminfo.target_price_high, color = color.green, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the lowest yearly price estimate.
    lowLine = line.new(time, close, YTD, syminfo.target_price_low, color = color.red, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the median yearly price estimate.
    medianLine = line.new(time, close, YTD, syminfo.target_price_median, color = color.gray, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the average yearly price estimate.
    averageLine = line.new(time, close, YTD, syminfo.target_price_average, color = color.orange, xloc = xloc.bar_time)
    // Fill the space between targets
    linefill.new(lowLine, medianLine, color.new(color.red, 90))
    linefill.new(medianLine, highLine, color.new(color.green, 90))
    // Create a label displaying the total number of analyst estimates.
    string estimatesText = str.format("Number of estimates: {0}", syminfo.target_price_estimates)
    label.new(bar_index, close, estimatesText, textcolor = color.white, size = size.large)
```

**REMARKS**

If analysts supply the targets when the market is closed, the variable can return na until the market opens.

**SEE ALSO**

syminfo.target_price_date, syminfo.target_price_estimates, syminfo.target_price_high, syminfo.target_price_low, syminfo.target_price_median

---

### syminfo.target_price_date

The starting date of the last price target prediction for the current symbol.

**TYPE**

series int

**EXAMPLE**

```pine
//@version=6
indicator("syminfo target_price")
if barstate.islastconfirmedhistory
    //@variable The time value one year from the date of the last analyst recommendations.
    int YTD = syminfo.target_price_date + timeframe.in_seconds("12M") * 1000
    //@variable A line connecting the current `close` to the highest yearly price estimate.
    highLine = line.new(time, close, YTD, syminfo.target_price_high, color = color.green, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the lowest yearly price estimate.
    lowLine = line.new(time, close, YTD, syminfo.target_price_low, color = color.red, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the median yearly price estimate.
    medianLine = line.new(time, close, YTD, syminfo.target_price_median, color = color.gray, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the average yearly price estimate.
    averageLine = line.new(time, close, YTD, syminfo.target_price_average, color = color.orange, xloc = xloc.bar_time)
    // Fill the space between targets
    linefill.new(lowLine, medianLine, color.new(color.red, 90))
    linefill.new(medianLine, highLine, color.new(color.green, 90))
    // Create a label displaying the total number of analyst estimates.
    string estimatesText = str.format("Number of estimates: {0}", syminfo.target_price_estimates)
    label.new(bar_index, close, estimatesText, textcolor = color.white, size = size.large)
```

**REMARKS**

If analysts supply the targets when the market is closed, the variable can return na until the market opens.

**SEE ALSO**

syminfo.target_price_average, syminfo.target_price_estimates, syminfo.target_price_high, syminfo.target_price_low, syminfo.target_price_median

---

### syminfo.target_price_estimates

The latest total number of price target predictions for the current symbol.

**TYPE**

series float

**EXAMPLE**

```pine
//@version=6
indicator("syminfo target_price")
if barstate.islastconfirmedhistory
    //@variable The time value one year from the date of the last analyst recommendations.
    int YTD = syminfo.target_price_date + timeframe.in_seconds("12M") * 1000
    //@variable A line connecting the current `close` to the highest yearly price estimate.
    highLine = line.new(time, close, YTD, syminfo.target_price_high, color = color.green, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the lowest yearly price estimate.
    lowLine = line.new(time, close, YTD, syminfo.target_price_low, color = color.red, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the median yearly price estimate.
    medianLine = line.new(time, close, YTD, syminfo.target_price_median, color = color.gray, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the average yearly price estimate.
    averageLine = line.new(time, close, YTD, syminfo.target_price_average, color = color.orange, xloc = xloc.bar_time)
    // Fill the space between targets
    linefill.new(lowLine, medianLine, color.new(color.red, 90))
    linefill.new(medianLine, highLine, color.new(color.green, 90))
    // Create a label displaying the total number of analyst estimates.
    string estimatesText = str.format("Number of estimates: {0}", syminfo.target_price_estimates)
    label.new(bar_index, close, estimatesText, textcolor = color.white, size = size.large)
```

**REMARKS**

If analysts supply the targets when the market is closed, the variable can return na until the market opens.

**SEE ALSO**

syminfo.target_price_average, syminfo.target_price_date, syminfo.target_price_high, syminfo.target_price_low, syminfo.target_price_median

---

### syminfo.target_price_high

The last highest yearly price target for the symbol predicted by analysts.

**TYPE**

series float

**EXAMPLE**

```pine
//@version=6
indicator("syminfo target_price")
if barstate.islastconfirmedhistory
    //@variable The time value one year from the date of the last analyst recommendations.
    int YTD = syminfo.target_price_date + timeframe.in_seconds("12M") * 1000
    //@variable A line connecting the current `close` to the highest yearly price estimate.
    highLine = line.new(time, close, YTD, syminfo.target_price_high, color = color.green, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the lowest yearly price estimate.
    lowLine = line.new(time, close, YTD, syminfo.target_price_low, color = color.red, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the median yearly price estimate.
    medianLine = line.new(time, close, YTD, syminfo.target_price_median, color = color.gray, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the average yearly price estimate.
    averageLine = line.new(time, close, YTD, syminfo.target_price_average, color = color.orange, xloc = xloc.bar_time)
    // Fill the space between targets
    linefill.new(lowLine, medianLine, color.new(color.red, 90))
    linefill.new(medianLine, highLine, color.new(color.green, 90))
    // Create a label displaying the total number of analyst estimates.
    string estimatesText = str.format("Number of estimates: {0}", syminfo.target_price_estimates)
    label.new(bar_index, close, estimatesText, textcolor = color.white, size = size.large)
```

**REMARKS**

If analysts supply the targets when the market is closed, the variable can return na until the market opens.

**SEE ALSO**

syminfo.target_price_average, syminfo.target_price_date, syminfo.target_price_estimates, syminfo.target_price_low, syminfo.target_price_median

---

### syminfo.target_price_low

The last lowest yearly price target for the symbol predicted by analysts.

**TYPE**

series float

**EXAMPLE**

```pine
//@version=6
indicator("syminfo target_price")
if barstate.islastconfirmedhistory
    //@variable The time value one year from the date of the last analyst recommendations.
    int YTD = syminfo.target_price_date + timeframe.in_seconds("12M") * 1000
    //@variable A line connecting the current `close` to the highest yearly price estimate.
    highLine = line.new(time, close, YTD, syminfo.target_price_high, color = color.green, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the lowest yearly price estimate.
    lowLine = line.new(time, close, YTD, syminfo.target_price_low, color = color.red, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the median yearly price estimate.
    medianLine = line.new(time, close, YTD, syminfo.target_price_median, color = color.gray, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the average yearly price estimate.
    averageLine = line.new(time, close, YTD, syminfo.target_price_average, color = color.orange, xloc = xloc.bar_time)
    // Fill the space between targets
    linefill.new(lowLine, medianLine, color.new(color.red, 90))
    linefill.new(medianLine, highLine, color.new(color.green, 90))
    // Create a label displaying the total number of analyst estimates.
    string estimatesText = str.format("Number of estimates: {0}", syminfo.target_price_estimates)
    label.new(bar_index, close, estimatesText, textcolor = color.white, size = size.large)
```

**REMARKS**

If analysts supply the targets when the market is closed, the variable can return na until the market opens.

**SEE ALSO**

syminfo.target_price_average, syminfo.target_price_date, syminfo.target_price_estimates, syminfo.target_price_high, syminfo.target_price_median

---

### syminfo.target_price_median

The median of the last yearly price targets for the symbol predicted by analysts.

**TYPE**

series float

**EXAMPLE**

```pine
//@version=6
indicator("syminfo target_price")
if barstate.islastconfirmedhistory
    //@variable The time value one year from the date of the last analyst recommendations.
    int YTD = syminfo.target_price_date + timeframe.in_seconds("12M") * 1000
    //@variable A line connecting the current `close` to the highest yearly price estimate.
    highLine = line.new(time, close, YTD, syminfo.target_price_high, color = color.green, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the lowest yearly price estimate.
    lowLine = line.new(time, close, YTD, syminfo.target_price_low, color = color.red, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the median yearly price estimate.
    medianLine = line.new(time, close, YTD, syminfo.target_price_median, color = color.gray, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the average yearly price estimate.
    averageLine = line.new(time, close, YTD, syminfo.target_price_average, color = color.orange, xloc = xloc.bar_time)
    // Fill the space between targets
    linefill.new(lowLine, medianLine, color.new(color.red, 90))
    linefill.new(medianLine, highLine, color.new(color.green, 90))
    // Create a label displaying the total number of analyst estimates.
    string estimatesText = str.format("Number of estimates: {0}", syminfo.target_price_estimates)
    label.new(bar_index, close, estimatesText, textcolor = color.white, size = size.large)
```

**REMARKS**

If analysts supply the targets when the market is closed, the variable can return na until the market opens.

**SEE ALSO**

syminfo.target_price_average, syminfo.target_price_date, syminfo.target_price_estimates, syminfo.target_price_high, syminfo.target_price_low

---

### syminfo.ticker

Symbol name without exchange prefix, e.g. 'MSFT'.

**TYPE**

simple string

**SEE ALSO**

syminfo.tickerid, timeframe.period, timeframe.multiplier, syminfo.root

---

### syminfo.tickerid

A ticker identifier representing the chart's symbol or a requested symbol, depending on how the script uses it. The variable's value represents a requested dataset's ticker ID when used in the expression argument of a request.*() function call. Otherwise, it represents the chart's ticker ID. The value contains an exchange prefix and a symbol name, separated by a colon (e.g., "NASDAQ:AAPL"). It can also include information about data modifications such as dividend adjustment, non-standard chart type, currency conversion, etc.

**TYPE**

simple string

**REMARKS**

Because the value of this variable does not always use a simple "prefix:ticker" format, it is a poor candidate for use in boolean comparisons or string manipulation functions. In those contexts, run the variable's result through ticker.standard to purify it. This will remove any extraneous information and return a ticker ID consistently formatted using the "prefix:ticker" structure.

To always access the script's main ticker ID, even within another context, use the syminfo.main_tickerid variable.

**SEE ALSO**

ticker.new, syminfo.main_tickerid, timeframe.main_period, syminfo.ticker, timeframe.period, timeframe.multiplier, syminfo.root

---

### syminfo.timezone

Timezone of the exchange of the chart main series. Possible values see in timestamp.

**TYPE**

simple string

**SEE ALSO**

timestamp

---

### syminfo.type

The type of market the symbol belongs to. The values are "stock", "fund", "dr", "right", "bond", "warrant", "structured", "index", "forex", "futures", "spread", "economic", "fundamental", "crypto", "spot", "swap", "option", "commodity".

**TYPE**

simple string

**SEE ALSO**

syminfo.ticker

---

### syminfo.volumetype

Volume type of the current symbol. Possible values are: "base" for base currency, "quote" for quote currency, "tick" for the number of transactions, and "n/a" when there is no volume or its type is not specified.

**TYPE**

simple string

**REMARKS**

Only some data feed suppliers provide information qualifying volume. As a result, the variable will return a value on some symbols only, mostly in the crypto sector.

**SEE ALSO**

syminfo.type

---

### ta.accdist

Accumulation/distribution index.

**TYPE**

series float

---

### ta.iii

Intraday Intensity Index.

**TYPE**

series float

**EXAMPLE**

```pine
//@version=6
indicator("Intraday Intensity Index")
plot(ta.iii, color=color.yellow)

// the same on pine
f_iii() =>
    (2 * close - high - low) / ((high - low) * volume)

plot(f_iii())
```

---

### ta.nvi

Negative Volume Index.

**TYPE**

series float

**EXAMPLE**

```pine
//@version=6
indicator("Negative Volume Index")

plot(ta.nvi, color=color.yellow)

// the same on pine
f_nvi() =>
    float ta_nvi = 1.0
    float prevNvi = (nz(ta_nvi[1], 0.0) == 0.0) ? 1.0 : ta_nvi[1]
    if nz(close, 0.0) == 0.0 or nz(close[1], 0.0) == 0.0
        ta_nvi := prevNvi
    else
        ta_nvi := (volume < nz(volume[1], 0.0)) ? prevNvi + ((close - close[1]) / close[1]) * prevNvi : prevNvi
    result = ta_nvi

plot(f_nvi())
```

---

### ta.obv

On Balance Volume.

**TYPE**

series float

**EXAMPLE**

```pine
//@version=6
indicator("On Balance Volume")
plot(ta.obv, color=color.yellow)

// the same on pine
f_obv() =>
    ta.cum(math.sign(ta.change(close)) * volume)

plot(f_obv())
```

---

### ta.pvi

Positive Volume Index.

**TYPE**

series float

**EXAMPLE**

```pine
//@version=6
indicator("Positive Volume Index")

plot(ta.pvi, color=color.yellow)

// the same on pine
f_pvi() =>
    float ta_pvi = 1.0
    float prevPvi = (nz(ta_pvi[1], 0.0) == 0.0) ? 1.0 : ta_pvi[1]
    if nz(close, 0.0) == 0.0 or nz(close[1], 0.0) == 0.0
        ta_pvi := prevPvi
    else
        ta_pvi := (volume > nz(volume[1], 0.0)) ? prevPvi + ((close - close[1]) / close[1]) * prevPvi : prevPvi
    result = ta_pvi

plot(f_pvi())
```

---

### ta.pvt

Price-Volume Trend.

**TYPE**

series float

**EXAMPLE**

```pine
//@version=6
indicator("Price-Volume Trend")
plot(ta.pvt, color=color.yellow)

// the same on pine
f_pvt() =>
    ta.cum((ta.change(close) / close[1]) * volume)

plot(f_pvt())
```

---

### ta.tr

True range, equivalent to ta.tr(handle_na = false). It is calculated as math.max(high - low, math.abs(high - close[1]), math.abs(low - close[1])).

**TYPE**

series float

**SEE ALSO**

ta.tr, ta.atr

---

### ta.vwap

Volume Weighted Average Price. It uses hlc3 as its source series.

**TYPE**

series float

**SEE ALSO**

ta.vwap

---

### ta.wad

Williams Accumulation/Distribution.

**TYPE**

series float

**EXAMPLE**

```pine
//@version=6
indicator("Williams Accumulation/Distribution")
plot(ta.wad, color=color.yellow)

// the same on pine
f_wad() =>
    trueHigh = math.max(high, close[1])
    trueLow = math.min(low, close[1])
    mom = ta.change(close)
    gain = (mom > 0) ? close - trueLow : (mom < 0) ? close - trueHigh : 0
    ta.cum(gain)

plot(f_wad())
```

---

### ta.wvad

Williams Variable Accumulation/Distribution.

**TYPE**

series float

**EXAMPLE**

```pine
//@version=6
indicator("Williams Variable Accumulation/Distribution")
plot(ta.wvad, color=color.yellow)

// the same on pine
f_wvad() =>
    (close - open) / (high - low) * volume

plot(f_wvad())
```

---

### table.all

Returns an array filled with all the current tables drawn by the script.

**TYPE**

array<table>

**EXAMPLE**

```pine
//@version=6
indicator("table.all")
//delete all tables
table.new(position = position.top_right, columns = 2, rows = 1, bgcolor = color.yellow, border_width = 1)
a_allTables = table.all
if array.size(a_allTables) > 0
    for i = 0 to array.size(a_allTables) - 1
        table.delete(array.get(a_allTables, i))
```

**REMARKS**

The array is read-only. Index zero of the array is the ID of the oldest object on the chart.

**SEE ALSO**

table.new, line.all, label.all, box.all

---

### time

Current bar time in UNIX format. It is the number of milliseconds that have elapsed since 00:00:00 UTC, 1 January 1970.

**TYPE**

series int

**REMARKS**

Note that this variable returns the timestamp based on the time of the bar's open. Because of that, for overnight sessions (e.g. EURUSD, where Monday session starts on Sunday, 17:00) this variable can return time before the specified date of the trading day. For example, on EURUSD, dayofmonth(time) can be lower by 1 than the date of the trading day, because the bar for the current day actually opens one day prior.

**SEE ALSO**

time, time_close, timenow, year, month, weekofyear, dayofmonth, dayofweek, hour, minute, second

---

### time_close

The time of the current bar's close in UNIX format. It represents the number of milliseconds elapsed since 00:00:00 UTC, 1 January 1970. On tick charts and price-based charts such as Renko, line break, Kagi, point & figure, and range, this variable's series holds an na timestamp for the latest realtime bar (because the future closing time is unpredictable), but valid timestamps for all previous bars.

**TYPE**

series int

**SEE ALSO**

time, timenow, year, month, weekofyear, dayofmonth, dayofweek, hour, minute, second

---

### time_tradingday

The timestamp that represents 00:00 UTC of the trading day the current bar belongs to, in UNIX format (the number of milliseconds that have elapsed since 00:00:00 UTC, 1 January 1970).

**TYPE**

series int

**EXAMPLE**

```pine
//@version=6
indicator("Friday session")

//@variable The day of week, based on the current `time_tradingday` value.
//          Uses "UTC+0" to return the daily session's timestamp at 00:00 UTC.
int tradingDayOfWeek = dayofweek(time_tradingday, "UTC+0")

//@variable Returns `true` if the `dayofweek` represents Friday, in exchange time.
//          It might never return `true` on overnight symbols, depending on the timeframe, since the Friday session
//          starts on Thursday.
bool isFriday = dayofweek == dayofweek.friday
//@variable Returns `true` if the `tradingDayOfWeek` is Friday.
//          Differs from `isFriday` on symbols with overnight sessions and for timeframes > "1D" on others.
bool isFridaySession = tradingDayOfWeek == dayofweek.friday

// Create a horizontal line at the `dayofweek.friday` value.
hline(dayofweek.friday, "Friday value", color.gray, hline.style_dashed, 2)
// Plot the `dayofweek` and `tradingDayOfWeek` for comparison.
plot(dayofweek, "Day of week", color.blue, 2)
plot(tradingDayOfWeek, "Trading day", color.teal, 3)
// Highlight the background when `isFriday` and `isFridaySession` occur.
bgcolor(isFriday ? color.new(color.blue, 90) : na, title = "isFriday highlight")
bgcolor(isFridaySession ? color.new(color.teal, 80) : na, title = "isFridaySession highlight")
```

**REMARKS**

This variable is helpful when working with overnight sessions, where the day's session can begin on the previous calendar day. For example, on the "FXCM:EURUSD" symbol, the Monday session starts on Sunday, 17:00, exchange time. Unlike time, which returns the timestamp for Sunday at 17:00 on the Monday daily bar, time_tradingday returns the timestamp for Monday at 00:00 UTC. When used on timeframes higher than "1D", time_tradingday returns the timestamp of the last trading day inside that bar (e.g., on "1W", it returns the timestamp of the final trading day within the week).

**SEE ALSO**

time, time_close

---

### timeframe.isdaily

Returns true if current resolution is a daily resolution, false otherwise.

**TYPE**

simple bool

**SEE ALSO**

timeframe.isdwm, timeframe.isintraday, timeframe.isminutes, timeframe.isseconds, timeframe.isticks, timeframe.isweekly, timeframe.ismonthly

---

### timeframe.isdwm

Returns true if current resolution is a daily or weekly or monthly resolution, false otherwise.

**TYPE**

simple bool

**SEE ALSO**

timeframe.isintraday, timeframe.isminutes, timeframe.isseconds, timeframe.isticks, timeframe.isdaily, timeframe.isweekly, timeframe.ismonthly

---

### timeframe.isintraday

Returns true if current resolution is an intraday (minutes or seconds) resolution, false otherwise.

**TYPE**

simple bool

**SEE ALSO**

timeframe.isminutes, timeframe.isseconds, timeframe.isticks, timeframe.isdwm, timeframe.isdaily, timeframe.isweekly, timeframe.ismonthly

---

### timeframe.isminutes

Returns true if current resolution is a minutes resolution, false otherwise.

**TYPE**

simple bool

**SEE ALSO**

timeframe.isdwm, timeframe.isintraday, timeframe.isseconds, timeframe.isticks, timeframe.isdaily, timeframe.isweekly, timeframe.ismonthly

---

### timeframe.ismonthly

Returns true if current resolution is a monthly resolution, false otherwise.

**TYPE**

simple bool

**SEE ALSO**

timeframe.isdwm, timeframe.isintraday, timeframe.isminutes, timeframe.isseconds, timeframe.isticks, timeframe.isdaily, timeframe.isweekly

---

### timeframe.isseconds

Returns true if current resolution is a seconds resolution, false otherwise.

**TYPE**

simple bool

**SEE ALSO**

timeframe.isdwm, timeframe.isintraday, timeframe.isminutes, timeframe.isticks, timeframe.isdaily, timeframe.isweekly, timeframe.ismonthly

---

### timeframe.isticks

Returns true if current resolution is a ticks resolution, false otherwise.

**TYPE**

simple bool

**SEE ALSO**

timeframe.isdwm, timeframe.isintraday, timeframe.isminutes, timeframe.isseconds, timeframe.isdaily, timeframe.isweekly, timeframe.ismonthly

---

### timeframe.isweekly

Returns true if current resolution is a weekly resolution, false otherwise.

**TYPE**

simple bool

**SEE ALSO**

timeframe.isdwm, timeframe.isintraday, timeframe.isminutes, timeframe.isseconds, timeframe.isticks, timeframe.isdaily, timeframe.ismonthly

---

### timeframe.main_period

A string representation of the script's main timeframe. If the script is an indicator that specifies a timeframe value in its declaration statement, this variable holds that value. Otherwise, its value represents the chart's timeframe. Unlike timeframe.period, this variable's value does not change when used in the expression argument of a request.*() function call.

The string's format is "<quantity>[<unit>]", where <unit> is "T" for ticks, "S" for seconds, "D" for days, "W" for weeks, and "M" for months, but is absent for minutes. No <unit> exists for hours: hourly timeframes are expressed in minutes.

The variable's value is: "10S" for 10 seconds, "30" for 30 minutes, "240" for four hours, "1D" for one day, "2W" for two weeks, and "3M" for one quarter.

**TYPE**

simple string

**SEE ALSO**

timeframe.period, syminfo.main_tickerid, syminfo.ticker, syminfo.tickerid, timeframe.multiplier

---

### timeframe.multiplier

Multiplier of resolution, e.g. '60' - 60, 'D' - 1, '5D' - 5, '12M' - 12.

**TYPE**

simple int

**SEE ALSO**

syminfo.ticker, syminfo.tickerid, timeframe.period

---

### timeframe.period

A string representation of the script's main timeframe or a requested timeframe, depending on how the script uses it. The variable's value represents the timeframe of a requested dataset when used in the expression argument of a request.*() function call. Otherwise, its value represents the script's main timeframe (timeframe.main_period), which equals either the timeframe argument of the indicator declaration statement or the chart's timeframe.

The string's format is "<quantity>[<unit>]", where <unit> is "T" for ticks, "S" for seconds, "D" for days, "W" for weeks, and "M" for months, but is absent for minutes. No <unit> exists for hours: hourly timeframes are expressed in minutes.

The variable's value is: "10S" for 10 seconds, "30" for 30 minutes, "240" for four hours, "1D" for one day, "2W" for two weeks, and "3M" for one quarter.

**TYPE**

simple string

**REMARKS**

To always access the script's main timeframe, even within another context, use the timeframe.main_period variable.

**SEE ALSO**

timeframe.main_period, syminfo.main_tickerid, syminfo.ticker, syminfo.tickerid, timeframe.multiplier

---

### timenow

Current time in UNIX format. It is the number of milliseconds that have elapsed since 00:00:00 UTC, 1 January 1970.

**TYPE**

series int

**REMARKS**

Please note that using this variable/function can cause indicator repainting.

**SEE ALSO**

timestamp, time, time_close, year, month, weekofyear, dayofmonth, dayofweek, hour, minute, second

---

### volume

Current bar volume.

**TYPE**

series float

**REMARKS**

Previous values may be accessed with square brackets operator [], e.g. volume[1], volume[2].

**SEE ALSO**

open, high, low, close, time, hl2, hlc3, hlcc4, ohlc4, ask, bid

---

### weekofyear

The week number of the year, in the exchange time zone, calculated from the bar's opening UNIX timestamp.

**TYPE**

series int

**REMARKS**

This variable always references the week number corresponding to the bar's opening time. Consequently, for symbols with overnight sessions (e.g., "EURUSD", where the "Monday" session starts on Sunday at 17:00 in exchange time), the value may represent a previous calendar week rather than the week of the session's primary trading day.

**SEE ALSO**

weekofyear, dayofmonth, dayofweek, time, year, month, hour, minute, second

---

### year

Current bar year in exchange timezone.

**TYPE**

series int

**REMARKS**

Note that this variable returns the year based on the time of the bar's open. For overnight sessions (e.g. EURUSD, where Monday session starts on Sunday, 17:00) this value can be lower by 1 than the year of the trading day.

**SEE ALSO**

year, time, month, weekofyear, dayofmonth, dayofweek, hour, minute, second
