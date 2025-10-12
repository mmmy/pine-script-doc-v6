# Constants

### adjustment.dividends

Constant for dividends adjustment type (dividends adjustment is applied).

**TYPE**

const string

**SEE ALSO**

adjustment.none, adjustment.splits, ticker.new

---

### adjustment.none

Constant for none adjustment type (no adjustment is applied).

**TYPE**

const string

**SEE ALSO**

adjustment.splits, adjustment.dividends, ticker.new

---

### adjustment.splits

Constant for splits adjustment type (splits adjustment is applied).

**TYPE**

const string

**SEE ALSO**

adjustment.none, adjustment.dividends, ticker.new

---

### alert.freq_all

A named constant for use with the freq parameter of the alert() function.

All function calls trigger the alert.

**TYPE**

const string

**SEE ALSO**

alert

---

### alert.freq_once_per_bar

A named constant for use with the freq parameter of the alert() function.

The first function call during the bar triggers the alert.

**TYPE**

const string

**SEE ALSO**

alert

---

### alert.freq_once_per_bar_close

A named constant for use with the freq parameter of the alert() function.

The function call triggers the alert only when it occurs during the last script iteration of the real-time bar, when it closes.

**TYPE**

const string

**SEE ALSO**

alert

---

### backadjustment.inherit

A constant to specify the value of the backadjustment parameter in ticker.new and ticker.modify functions.

**TYPE**

const backadjustment

**SEE ALSO**

ticker.new, ticker.modify, backadjustment.on, backadjustment.off

---

### backadjustment.off

A constant to specify the value of the backadjustment parameter in ticker.new and ticker.modify functions.

**TYPE**

const backadjustment

**SEE ALSO**

ticker.new, ticker.modify, backadjustment.on, backadjustment.inherit

---

### backadjustment.on

A constant to specify the value of the backadjustment parameter in ticker.new and ticker.modify functions.

**TYPE**

const backadjustment

**SEE ALSO**

ticker.new, ticker.modify, backadjustment.inherit, backadjustment.off

---

### barmerge.gaps_off

Merge strategy for requested data. Data is merged continuously without gaps, all the gaps are filled with the previous nearest existing value.

**TYPE**

const barmerge_gaps

**SEE ALSO**

request.security, barmerge.gaps_on

---

### barmerge.gaps_on

Merge strategy for requested data. Data is merged with possible gaps (na values).

**TYPE**

const barmerge_gaps

**SEE ALSO**

request.security, barmerge.gaps_off

---

### barmerge.lookahead_off

Merge strategy for the requested data position. Requested barset is merged with current barset in the order of sorting bars by their close time. This merge strategy disables effect of getting data from "future" on calculation on history.

**TYPE**

const barmerge_lookahead

**SEE ALSO**

request.security, barmerge.lookahead_on

---

### barmerge.lookahead_on

Merge strategy for the requested data position. Requested barset is merged with current barset in the order of sorting bars by their opening time. This merge strategy can lead to undesirable effect of getting data from "future" on calculation on history. This is unacceptable in backtesting strategies, but can be useful in indicators.

**TYPE**

const barmerge_lookahead

**SEE ALSO**

request.security, barmerge.lookahead_off

---

### color.aqua

Is a named constant for #00BCD4 color.

**TYPE**

const color

**SEE ALSO**

color.black, color.silver, color.gray, color.white, color.maroon, color.red, color.purple, color.fuchsia, color.green, color.lime, color.olive, color.yellow, color.navy, color.blue, color.teal, color.orange

---

### color.black

Is a named constant for #363A45 color.

**TYPE**

const color

**SEE ALSO**

color.silver, color.gray, color.white, color.maroon, color.red, color.purple, color.fuchsia, color.green, color.lime, color.olive, color.yellow, color.navy, color.blue, color.teal, color.aqua, color.orange

---

### color.blue

Is a named constant for #2962ff color.

**TYPE**

const color

**SEE ALSO**

color.black, color.silver, color.gray, color.white, color.maroon, color.red, color.purple, color.fuchsia, color.green, color.lime, color.olive, color.yellow, color.navy, color.teal, color.aqua, color.orange

---

### color.fuchsia

Is a named constant for #E040FB color.

**TYPE**

const color

**SEE ALSO**

color.black, color.silver, color.gray, color.white, color.maroon, color.red, color.purple, color.green, color.lime, color.olive, color.yellow, color.navy, color.blue, color.teal, color.aqua, color.orange

---

### color.gray

Is a named constant for #787B86 color.

**TYPE**

const color

**SEE ALSO**

color.black, color.silver, color.white, color.maroon, color.red, color.purple, color.fuchsia, color.green, color.lime, color.olive, color.yellow, color.navy, color.blue, color.teal, color.aqua, color.orange

---

### color.green

Is a named constant for #4CAF50 color.

**TYPE**

const color

**SEE ALSO**

color.black, color.silver, color.gray, color.white, color.maroon, color.red, color.purple, color.fuchsia, color.lime, color.olive, color.yellow, color.navy, color.blue, color.teal, color.aqua, color.orange

---

### color.lime

Is a named constant for #00E676 color.

**TYPE**

const color

**SEE ALSO**

color.black, color.silver, color.gray, color.white, color.maroon, color.red, color.purple, color.fuchsia, color.green, color.olive, color.yellow, color.navy, color.blue, color.teal, color.aqua, color.orange

---

### color.maroon

Is a named constant for #880E4F color.

**TYPE**

const color

**SEE ALSO**

color.black, color.silver, color.gray, color.white, color.red, color.purple, color.fuchsia, color.green, color.lime, color.olive, color.yellow, color.navy, color.blue, color.teal, color.aqua, color.orange

---

### color.navy

Is a named constant for #311B92 color.

**TYPE**

const color

**SEE ALSO**

color.black, color.silver, color.gray, color.white, color.maroon, color.red, color.purple, color.fuchsia, color.green, color.lime, color.olive, color.yellow, color.blue, color.teal, color.aqua, color.orange

---

### color.olive

Is a named constant for #808000 color.

**TYPE**

const color

**SEE ALSO**

color.black, color.silver, color.gray, color.white, color.maroon, color.red, color.purple, color.fuchsia, color.green, color.lime, color.yellow, color.navy, color.blue, color.teal, color.aqua, color.orange

---

### color.orange

Is a named constant for #FF9800 color.

**TYPE**

const color

**SEE ALSO**

color.black, color.silver, color.gray, color.white, color.maroon, color.red, color.purple, color.fuchsia, color.green, color.lime, color.olive, color.yellow, color.navy, color.blue, color.teal, color.aqua

---

### color.purple

Is a named constant for #9C27B0 color.

**TYPE**

const color

**SEE ALSO**

color.black, color.silver, color.gray, color.white, color.maroon, color.red, color.fuchsia, color.green, color.lime, color.olive, color.yellow, color.navy, color.blue, color.teal, color.aqua, color.orange

---

### color.red

Is a named constant for #F23645 color.

**TYPE**

const color

**SEE ALSO**

color.black, color.silver, color.gray, color.white, color.maroon, color.purple, color.fuchsia, color.green, color.lime, color.olive, color.yellow, color.navy, color.blue, color.teal, color.aqua, color.orange

---

### color.silver

Is a named constant for #B2B5BE color.

**TYPE**

const color

**SEE ALSO**

color.black, color.gray, color.white, color.maroon, color.red, color.purple, color.fuchsia, color.green, color.lime, color.olive, color.yellow, color.navy, color.blue, color.teal, color.aqua, color.orange

---

### color.teal

Is a named constant for #089981 color.

**TYPE**

const color

**SEE ALSO**

color.black, color.silver, color.gray, color.white, color.maroon, color.red, color.purple, color.fuchsia, color.green, color.lime, color.olive, color.yellow, color.navy, color.blue, color.aqua, color.orange

---

### color.white

Is a named constant for #FFFFFF color.

**TYPE**

const color

**SEE ALSO**

color.black, color.silver, color.gray, color.maroon, color.red, color.purple, color.fuchsia, color.green, color.lime, color.olive, color.yellow, color.navy, color.blue, color.teal, color.aqua, color.orange

---

### color.yellow

Is a named constant for #FDD835 color.

**TYPE**

const color

**SEE ALSO**

color.black, color.silver, color.gray, color.white, color.maroon, color.red, color.purple, color.fuchsia, color.green, color.lime, color.olive, color.navy, color.blue, color.teal, color.aqua, color.orange

---

### currency.AED

Arab Emirates Dirham.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.ARS

Argentine Pesos.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.AUD

Australian dollar.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.BDT

Bangladeshi Taka.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.BHD

Bahraini Dinar.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.BRL

Brazilian real.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.BTC

Bitcoin.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.CAD

Canadian dollar.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.CHF

Swiss franc.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.CLP

Chilean Peso.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.CNY

Chinese Yuan.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.COP

Colombian Peso.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.CZK

Czech Koruna.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.DKK

Danish Krone.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.EGP

Egyptian pound.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.ETH

Ethereum.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.EUR

Euro.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.GBP

Pound sterling.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.HKD

Hong Kong dollar.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.HUF

Hungarian Forint.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.IDR

Indonesian Rupiah.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.ILS

Israeli New Shekel.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.INR

Indian rupee.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.ISK

Icelandic Krona.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.JPY

Japanese yen.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.KES

Kenyan Shilling.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.KRW

South Korean won.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.KWD

Kuwaiti Dinar.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.LKR

Sri Lankan Rupee.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.MAD

Moroccan Dirham.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.MXN

Mexican Peso.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.MYR

Malaysian ringgit.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.NGN

Nigerian Naira.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.NOK

Norwegian krone.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.NONE

Unspecified currency.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.NZD

New Zealand dollar.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.PEN

Peruvian sol.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.PHP

Philippine Peso.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.PKR

Pakistani rupee.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.PLN

Polish zloty.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.QAR

Qatari Riyal.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.RON

Romanian Leu.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.RSD

Serbian Dinar.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.RUB

Russian ruble.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.SAR

Saudi Riyal.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.SEK

Swedish krona.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.SGD

Singapore dollar.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.THB

Thai Baht.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.TND

Tunisian Dinar.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.TRY

Turkish lira.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.TWD

New Taiwan Dollar.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.USD

United States dollar.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.USDT

Tether.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.VES

Venezuelan Bolivar.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.VND

Vietnamese Dong.

**TYPE**

const string

**SEE ALSO**

strategy

---

### currency.ZAR

South African rand.

**TYPE**

const string

**SEE ALSO**

strategy

---

### dayofweek.friday

Is a named constant for return value of dayofweek function and value of dayofweek variable.

**TYPE**

const int

**SEE ALSO**

dayofweek.sunday, dayofweek.monday, dayofweek.tuesday, dayofweek.wednesday, dayofweek.thursday, dayofweek.saturday

---

### dayofweek.monday

Is a named constant for return value of dayofweek function and value of dayofweek variable.

**TYPE**

const int

**SEE ALSO**

dayofweek.sunday, dayofweek.tuesday, dayofweek.wednesday, dayofweek.thursday, dayofweek.friday, dayofweek.saturday

---

### dayofweek.saturday

Is a named constant for return value of dayofweek function and value of dayofweek variable.

**TYPE**

const int

**SEE ALSO**

dayofweek.sunday, dayofweek.monday, dayofweek.tuesday, dayofweek.wednesday, dayofweek.thursday, dayofweek.friday

---

### dayofweek.sunday

Is a named constant for return value of dayofweek function and value of dayofweek variable.

**TYPE**

const int

**SEE ALSO**

dayofweek.monday, dayofweek.tuesday, dayofweek.wednesday, dayofweek.thursday, dayofweek.friday, dayofweek.saturday

---

### dayofweek.thursday

Is a named constant for return value of dayofweek function and value of dayofweek variable.

**TYPE**

const int

**SEE ALSO**

dayofweek.sunday, dayofweek.monday, dayofweek.tuesday, dayofweek.wednesday, dayofweek.friday, dayofweek.saturday

---

### dayofweek.tuesday

Is a named constant for return value of dayofweek function and value of dayofweek variable.

**TYPE**

const int

**SEE ALSO**

dayofweek.sunday, dayofweek.monday, dayofweek.wednesday, dayofweek.thursday, dayofweek.friday, dayofweek.saturday

---

### dayofweek.wednesday

Is a named constant for return value of dayofweek function and value of dayofweek variable.

**TYPE**

const int

**SEE ALSO**

dayofweek.sunday, dayofweek.monday, dayofweek.tuesday, dayofweek.thursday, dayofweek.friday, dayofweek.saturday

---

### display.all

A named constant for use with the display parameter of plot*() and input*() functions. Displays plotted or input values in all possible locations.

**TYPE**

const plot_simple_display

**SEE ALSO**

plot, plotshape, plotchar, plotarrow, plotbar, plotcandle

---

### display.data_window

A named constant for use with the display parameter of plot*() and input*() functions. Displays plotted or input values in the Data Window, a menu accessible from the chart's right sidebar.

**TYPE**

const plot_display

**SEE ALSO**

plot, plotshape, plotchar, plotarrow, plotbar, plotcandle

---

### display.none

A named constant for use with the display parameter of plot*() and input*() functions. plot*() functions using this will not display their plotted values anywhere. However, alert template messages and fill functions can still use the values, and they will appear in exported chart data. input*() functions using this constant will only display their values within the script's settings.

**TYPE**

const plot_simple_display

**SEE ALSO**

plot, plotshape, plotchar, plotarrow, plotbar, plotcandle

---

### display.pane

A named constant for use with the display parameter of plot*() functions. Displays plotted values in the chart pane used by the script.

**TYPE**

const plot_display

**SEE ALSO**

plot, plotshape, plotchar, plotarrow, plotbar, plotcandle

---

### display.price_scale

A named constant for use with the display parameter of plot*() functions. Displays the plot’s label and value on the price scale if the chart's settings allow it.

**TYPE**

const plot_display

**SEE ALSO**

plot, plotshape, plotchar, plotarrow, plotbar, plotcandle

---

### display.status_line

A named constant for use with the display parameter of plot*() and input*() functions. Displays plotted or input values in the status line next to the script's name on the chart if the chart's settings allow it.

**TYPE**

const plot_display

**SEE ALSO**

plot, plotshape, plotchar, plotarrow, plotbar, plotcandle

---

### dividends.gross

A named constant for the request.dividends function. Is used to request the dividends return on a stock before deductions.

**TYPE**

const string

**SEE ALSO**

request.dividends

---

### dividends.net

A named constant for the request.dividends function. Is used to request the dividends return on a stock after deductions.

**TYPE**

const string

**SEE ALSO**

request.dividends

---

### earnings.actual

A named constant for the request.earnings function. Is used to request the earnings value as it was reported.

**TYPE**

const string

**SEE ALSO**

request.earnings

---

### earnings.estimate

A named constant for the request.earnings function. Is used to request the estimated earnings value.

**TYPE**

const string

**SEE ALSO**

request.earnings

---

### earnings.standardized

A named constant for the request.earnings function. Is used to request the standardized earnings value.

**TYPE**

const string

**SEE ALSO**

request.earnings

---

### extend.both

A named constant for line.new and line.set_extend functions.

**TYPE**

const string

**SEE ALSO**

line.new, line.set_extend, extend.none, extend.left, extend.right

---

### extend.left

A named constant for line.new and line.set_extend functions.

**TYPE**

const string

**SEE ALSO**

line.new, line.set_extend, extend.none, extend.right, extend.both

---

### extend.none

A named constant for line.new and line.set_extend functions.

**TYPE**

const string

**SEE ALSO**

line.new, line.set_extend, extend.left, extend.right, extend.both

---

### extend.right

A named constant for line.new and line.set_extend functions.

**TYPE**

const string

**SEE ALSO**

line.new, line.set_extend, extend.none, extend.left, extend.both

---

### false

Literal representing a bool value, and result of a comparison operation.

**REMARKS**

See the User Manual for comparison operators and logical operators.

**SEE ALSO**

bool

---

### font.family_default

Default text font for box.new, box.set_text_font_family, label.new, label.set_text_font_family, table.cell and table.cell_set_text_font_family functions.

**TYPE**

const string

**SEE ALSO**

box.new, box.set_text_font_family, label.new, label.set_text_font_family, table.cell, table.cell_set_text_font_family, font.family_monospace

---

### font.family_monospace

Monospace text font for box.new, box.set_text_font_family, label.new, label.set_text_font_family, table.cell and table.cell_set_text_font_family functions.

**TYPE**

const string

**SEE ALSO**

box.new, box.set_text_font_family, label.new, label.set_text_font_family, table.cell, table.cell_set_text_font_family, font.family_default

---

### format.inherit

Is a named constant for selecting the formatting of the script output values from the parent series in the indicator function.

**TYPE**

const string

**SEE ALSO**

indicator, format.price, format.volume, format.percent

---

### format.mintick

Is a named constant to use with the str.tostring function. Passing a number to str.tostring with this argument rounds the number to the nearest value that can be divided by syminfo.mintick, without the remainder, with ties rounding up, and returns the string version of said value with trailing zeros.

**TYPE**

const string

**SEE ALSO**

indicator, format.inherit, format.price, format.volume

---

### format.percent

Is a named constant for selecting the formatting of the script output values as a percentage in the indicator function. It adds a percent sign after values.

**TYPE**

const string

**REMARKS**

The default precision is 2, regardless of the precision of the chart itself. This can be changed with the 'precision' argument of the indicator function.

**SEE ALSO**

indicator, format.inherit, format.price, format.volume

---

### format.price

Is a named constant for selecting the formatting of the script output values as prices in the indicator function.

**TYPE**

const string

**REMARKS**

If format is format.price, default precision value is set. You can use the precision argument of indicator function to change the precision value.

**SEE ALSO**

indicator, format.inherit, format.volume, format.percent

---

### format.volume

Is a named constant for selecting the formatting of the script output values as volume in the indicator function, e.g. '5183' will be formatted as '5.183K'.

The decimal precision rules defined by this variable take precedence over other precision settings. When an indicator, strategy, or plot*() call uses this format option, the function's precision parameter will not affect the result.

**TYPE**

const string

**SEE ALSO**

indicator, format.inherit, format.price, format.percent

---

### hline.style_dashed

Is a named constant for dashed linestyle of hline function.

**TYPE**

const hline_style

**SEE ALSO**

hline.style_solid, hline.style_dotted

---

### hline.style_dotted

Is a named constant for dotted linestyle of hline function.

**TYPE**

const hline_style

**SEE ALSO**

hline.style_solid, hline.style_dashed

---

### hline.style_solid

Is a named constant for solid linestyle of hline function.

**TYPE**

const hline_style

**SEE ALSO**

hline.style_dotted, hline.style_dashed

---

### label.style_arrowdown

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_none, label.style_xcross, label.style_cross, label.style_triangleup, label.style_triangledown, label.style_flag, label.style_circle, label.style_arrowup, label.style_label_up, label.style_label_down, label.style_label_left, label.style_label_right, label.style_label_lower_left, label.style_label_lower_right, label.style_label_upper_left, label.style_label_upper_right, label.style_label_center, label.style_square, label.style_diamond

---

### label.style_arrowup

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_none, label.style_xcross, label.style_cross, label.style_triangleup, label.style_triangledown, label.style_flag, label.style_circle, label.style_arrowdown, label.style_label_up, label.style_label_down, label.style_label_left, label.style_label_right, label.style_label_lower_left, label.style_label_lower_right, label.style_label_upper_left, label.style_label_upper_right, label.style_label_center, label.style_square, label.style_diamond

---

### label.style_circle

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_none, label.style_xcross, label.style_cross, label.style_triangleup, label.style_triangledown, label.style_flag, label.style_arrowup, label.style_arrowdown, label.style_label_up, label.style_label_down, label.style_label_left, label.style_label_right, label.style_label_lower_left, label.style_label_lower_right, label.style_label_upper_left, label.style_label_upper_right, label.style_label_center, label.style_square, label.style_diamond

---

### label.style_cross

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_none, label.style_xcross, label.style_triangleup, label.style_triangledown, label.style_flag, label.style_circle, label.style_arrowup, label.style_arrowdown, label.style_label_up, label.style_label_down, label.style_label_left, label.style_label_right, label.style_label_lower_left, label.style_label_lower_right, label.style_label_upper_left, label.style_label_upper_right, label.style_label_center, label.style_square, label.style_diamond

---

### label.style_diamond

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_none, label.style_xcross, label.style_cross, label.style_triangleup, label.style_triangledown, label.style_flag, label.style_circle, label.style_arrowup, label.style_arrowdown, label.style_label_up, label.style_label_down, label.style_label_left, label.style_label_right, label.style_label_lower_left, label.style_label_lower_right, label.style_label_upper_left, label.style_label_upper_right, label.style_label_center, label.style_square

---

### label.style_flag

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_none, label.style_xcross, label.style_cross, label.style_triangleup, label.style_triangledown, label.style_circle, label.style_arrowup, label.style_arrowdown, label.style_label_up, label.style_label_down, label.style_label_left, label.style_label_right, label.style_label_lower_left, label.style_label_lower_right, label.style_label_upper_left, label.style_label_upper_right, label.style_label_center, label.style_square, label.style_diamond

---

### label.style_label_center

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_none, label.style_xcross, label.style_cross, label.style_triangleup, label.style_triangledown, label.style_flag, label.style_circle, label.style_arrowup, label.style_arrowdown, label.style_label_up, label.style_label_down, label.style_label_left, label.style_label_right, label.style_label_lower_left, label.style_label_lower_right, label.style_label_upper_left, label.style_label_upper_right, label.style_square, label.style_diamond

---

### label.style_label_down

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_none, label.style_xcross, label.style_cross, label.style_triangleup, label.style_triangledown, label.style_flag, label.style_circle, label.style_arrowup, label.style_arrowdown, label.style_label_up, label.style_label_left, label.style_label_right, label.style_label_lower_left, label.style_label_lower_right, label.style_label_upper_left, label.style_label_upper_right, label.style_label_center, label.style_square, label.style_diamond

---

### label.style_label_left

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_none, label.style_xcross, label.style_cross, label.style_triangleup, label.style_triangledown, label.style_flag, label.style_circle, label.style_arrowup, label.style_arrowdown, label.style_label_up, label.style_label_down, label.style_label_right, label.style_label_lower_left, label.style_label_lower_right, label.style_label_upper_left, label.style_label_upper_right, label.style_label_center, label.style_square, label.style_diamond

---

### label.style_label_lower_left

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_none, label.style_xcross, label.style_cross, label.style_triangleup, label.style_triangledown, label.style_flag, label.style_circle, label.style_arrowup, label.style_arrowdown, label.style_label_up, label.style_label_down, label.style_label_left, label.style_label_right, label.style_label_lower_right, label.style_label_upper_left, label.style_label_upper_right, label.style_label_center, label.style_square, label.style_diamond

---

### label.style_label_lower_right

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_none, label.style_xcross, label.style_cross, label.style_triangleup, label.style_triangledown, label.style_flag, label.style_circle, label.style_arrowup, label.style_arrowdown, label.style_label_up, label.style_label_down, label.style_label_left, label.style_label_right, label.style_label_lower_left, label.style_label_upper_left, label.style_label_upper_right, label.style_label_center, label.style_square, label.style_diamond

---

### label.style_label_right

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_none, label.style_xcross, label.style_cross, label.style_triangleup, label.style_triangledown, label.style_flag, label.style_circle, label.style_arrowup, label.style_arrowdown, label.style_label_up, label.style_label_down, label.style_label_left, label.style_label_lower_left, label.style_label_lower_right, label.style_label_upper_left, label.style_label_upper_right, label.style_label_center, label.style_square, label.style_diamond

---

### label.style_label_up

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_none, label.style_xcross, label.style_cross, label.style_triangleup, label.style_triangledown, label.style_flag, label.style_circle, label.style_arrowup, label.style_arrowdown, label.style_label_down, label.style_label_left, label.style_label_right, label.style_label_lower_left, label.style_label_lower_right, label.style_label_upper_left, label.style_label_upper_right, label.style_label_center, label.style_square, label.style_diamond

---

### label.style_label_upper_left

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_none, label.style_xcross, label.style_cross, label.style_triangleup, label.style_triangledown, label.style_flag, label.style_circle, label.style_arrowup, label.style_arrowdown, label.style_label_up, label.style_label_down, label.style_label_left, label.style_label_right, label.style_label_lower_left, label.style_label_lower_right, label.style_label_upper_right, label.style_label_center, label.style_square, label.style_diamond

---

### label.style_label_upper_right

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_none, label.style_xcross, label.style_cross, label.style_triangleup, label.style_triangledown, label.style_flag, label.style_circle, label.style_arrowup, label.style_arrowdown, label.style_label_up, label.style_label_down, label.style_label_left, label.style_label_right, label.style_label_lower_left, label.style_label_lower_right, label.style_label_upper_left, label.style_label_center, label.style_square, label.style_diamond

---

### label.style_none

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_xcross, label.style_cross, label.style_triangleup, label.style_triangledown, label.style_flag, label.style_circle, label.style_arrowup, label.style_arrowdown, label.style_label_up, label.style_label_down, label.style_label_left, label.style_label_right, label.style_label_center, label.style_square, label.style_diamond

---

### label.style_square

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_none, label.style_xcross, label.style_cross, label.style_triangleup, label.style_triangledown, label.style_flag, label.style_circle, label.style_arrowup, label.style_arrowdown, label.style_label_up, label.style_label_down, label.style_label_left, label.style_label_right, label.style_label_lower_left, label.style_label_lower_right, label.style_label_upper_left, label.style_label_upper_right, label.style_label_center, label.style_diamond

---

### label.style_text_outline

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_none, label.style_xcross, label.style_cross, label.style_triangleup, label.style_triangledown, label.style_flag, label.style_circle, label.style_arrowup, label.style_arrowdown, label.style_label_up, label.style_label_down, label.style_label_left, label.style_label_right, label.style_label_lower_left, label.style_label_lower_right, label.style_label_upper_left, label.style_label_upper_right, label.style_label_center, label.style_square, label.style_diamond

---

### label.style_triangledown

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_none, label.style_xcross, label.style_cross, label.style_triangleup, label.style_flag, label.style_circle, label.style_arrowup, label.style_arrowdown, label.style_label_up, label.style_label_down, label.style_label_left, label.style_label_right, label.style_label_lower_left, label.style_label_lower_right, label.style_label_upper_left, label.style_label_upper_right, label.style_label_center, label.style_square, label.style_diamond

---

### label.style_triangleup

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_none, label.style_xcross, label.style_cross, label.style_triangledown, label.style_flag, label.style_circle, label.style_arrowup, label.style_arrowdown, label.style_label_up, label.style_label_down, label.style_label_left, label.style_label_right, label.style_label_lower_left, label.style_label_lower_right, label.style_label_upper_left, label.style_label_upper_right, label.style_label_center, label.style_square, label.style_diamond

---

### label.style_xcross

Label style for label.new and label.set_style functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, label.set_textalign, label.style_none, label.style_cross, label.style_triangleup, label.style_triangledown, label.style_flag, label.style_circle, label.style_arrowup, label.style_arrowdown, label.style_label_up, label.style_label_down, label.style_label_left, label.style_label_right, label.style_label_center, label.style_square, label.style_diamond

---

### line.style_arrow_both

Line style for line.new and line.set_style functions. Solid line with arrows on both points.

**TYPE**

const string

**SEE ALSO**

line.new, line.set_style, line.style_solid, line.style_dotted, line.style_dashed, line.style_arrow_left, line.style_arrow_right

---

### line.style_arrow_left

Line style for line.new and line.set_style functions. Solid line with arrow on the first point.

**TYPE**

const string

**SEE ALSO**

line.new, line.set_style, line.style_solid, line.style_dotted, line.style_dashed, line.style_arrow_right, line.style_arrow_both

---

### line.style_arrow_right

Line style for line.new and line.set_style functions. Solid line with arrow on the second point.

**TYPE**

const string

**SEE ALSO**

line.new, line.set_style, line.style_solid, line.style_dotted, line.style_dashed, line.style_arrow_left, line.style_arrow_both

---

### line.style_dashed

Line style for line.new and line.set_style functions.

**TYPE**

const string

**SEE ALSO**

line.new, line.set_style, line.style_solid, line.style_dotted, line.style_arrow_left, line.style_arrow_right, line.style_arrow_both

---

### line.style_dotted

Line style for line.new and line.set_style functions.

**TYPE**

const string

**SEE ALSO**

line.new, line.set_style, line.style_solid, line.style_dashed, line.style_arrow_left, line.style_arrow_right, line.style_arrow_both

---

### line.style_solid

Line style for line.new and line.set_style functions.

**TYPE**

const string

**SEE ALSO**

line.new, line.set_style, line.style_dotted, line.style_dashed, line.style_arrow_left, line.style_arrow_right, line.style_arrow_both

---

### location.abovebar

Location value for plotshape, plotchar functions. Shape is plotted above main series bars.

**TYPE**

const string

**SEE ALSO**

plotshape, plotchar, location.belowbar, location.top, location.bottom, location.absolute

---

### location.absolute

Location value for plotshape, plotchar functions. Shape is plotted on chart using indicator value as a price coordinate.

**TYPE**

const string

**SEE ALSO**

plotshape, plotchar, location.abovebar, location.belowbar, location.top, location.bottom

---

### location.belowbar

Location value for plotshape, plotchar functions. Shape is plotted below main series bars.

**TYPE**

const string

**SEE ALSO**

plotshape, plotchar, location.abovebar, location.top, location.bottom, location.absolute

---

### location.bottom

Location value for plotshape, plotchar functions. Shape is plotted near the bottom chart border.

**TYPE**

const string

**SEE ALSO**

plotshape, plotchar, location.abovebar, location.belowbar, location.top, location.absolute

---

### location.top

Location value for plotshape, plotchar functions. Shape is plotted near the top chart border.

**TYPE**

const string

**SEE ALSO**

plotshape, plotchar, location.abovebar, location.belowbar, location.bottom, location.absolute

---

### math.e

Is a named constant for Euler's number. It is equal to 2.7182818284590452.

**TYPE**

const float

**SEE ALSO**

math.phi, math.pi, math.rphi

---

### math.phi

Is a named constant for the golden ratio. It is equal to 1.6180339887498948.

**TYPE**

const float

**SEE ALSO**

math.e, math.pi, math.rphi

---

### math.pi

Is a named constant for Archimedes' constant. It is equal to 3.1415926535897932.

**TYPE**

const float

**SEE ALSO**

math.e, math.phi, math.rphi

---

### math.rphi

Is a named constant for the golden ratio conjugate. It is equal to 0.6180339887498948.

**TYPE**

const float

**SEE ALSO**

math.e, math.pi, math.phi

---

### order.ascending

Determines the sort order of the array from the smallest to the largest value.

**TYPE**

const sort_order

**SEE ALSO**

array.new_float, array.sort

---

### order.descending

Determines the sort order of the array from the largest to the smallest value.

**TYPE**

const sort_order

**SEE ALSO**

array.new_float, array.sort

---

### plot.linestyle_dashed

A named constant for use with the plot function's linestyle parameter, which modifies the appearance of plotted lines. If the style argument of the function call specifies a plot style that displays a line, using this constant as the linestyle argument specifies that the plotted line is dashed.

**TYPE**

const plot_line_style

**SEE ALSO**

plot, plot.linestyle_solid, plot.linestyle_dotted

---

### plot.linestyle_dotted

A named constant for use with the plot function's linestyle parameter, which modifies the appearance of plotted lines. If the style argument of the function call specifies a plot style that displays a line, using this constant as the linestyle argument specifies that the plotted line is dotted.

**TYPE**

const plot_line_style

**SEE ALSO**

plot, plot.linestyle_dashed, plot.linestyle_solid

---

### plot.linestyle_solid

A named constant for use with the plot function's linestyle parameter, which modifies the appearance of plotted lines. If the style argument of the function call specifies a plot style that displays a line, using this constant as the linestyle argument specifies that the plotted line is solid.

**TYPE**

const plot_line_style

**SEE ALSO**

plot, plot.linestyle_dashed, plot.linestyle_dotted

---

### plot.style_area

A named constant for the 'Area' style, to be used as an argument for the style parameter in the plot function.

**TYPE**

const plot_style

**SEE ALSO**

plot, plot.style_line, plot.style_linebr, plot.style_histogram, plot.style_cross, plot.style_areabr, plot.style_columns, plot.style_circles, plot.style_stepline, plot.style_stepline_diamond, plot.style_steplinebr

---

### plot.style_areabr

A named constant for the 'Area With Breaks' style, to be used as an argument for the style parameter in the plot function. Similar to plot.style_area, except the gaps in the data are not filled.

**TYPE**

const plot_style

**SEE ALSO**

plot, plot.style_line, plot.style_linebr, plot.style_histogram, plot.style_cross, plot.style_area, plot.style_columns, plot.style_circles, plot.style_stepline, plot.style_stepline_diamond, plot.style_steplinebr

---

### plot.style_circles

A named constant for the 'Circles' style, to be used as an argument for the style parameter in the plot function.

**TYPE**

const plot_style

**SEE ALSO**

plot, plot.style_line, plot.style_linebr, plot.style_histogram, plot.style_cross, plot.style_area, plot.style_areabr, plot.style_columns, plot.style_stepline, plot.style_stepline_diamond, plot.style_steplinebr

---

### plot.style_columns

A named constant for the 'Columns' style, to be used as an argument for the style parameter in the plot function.

**TYPE**

const plot_style

**SEE ALSO**

plot, plot.style_line, plot.style_linebr, plot.style_histogram, plot.style_cross, plot.style_area, plot.style_areabr, plot.style_circles, plot.style_stepline, plot.style_stepline_diamond, plot.style_steplinebr

---

### plot.style_cross

A named constant for the 'Cross' style, to be used as an argument for the style parameter in the plot function.

**TYPE**

const plot_style

**SEE ALSO**

plot, plot.style_line, plot.style_linebr, plot.style_histogram, plot.style_area, plot.style_areabr, plot.style_columns, plot.style_circles, plot.style_stepline, plot.style_stepline_diamond, plot.style_steplinebr

---

### plot.style_histogram

A named constant for the 'Histogram' style, to be used as an argument for the style parameter in the plot function.

**TYPE**

const plot_style

**SEE ALSO**

plot, plot.style_line, plot.style_linebr, plot.style_cross, plot.style_area, plot.style_areabr, plot.style_columns, plot.style_circles, plot.style_stepline, plot.style_stepline_diamond, plot.style_steplinebr

---

### plot.style_line

A named constant for the 'Line' style, to be used as an argument for the style parameter in the plot function.

**TYPE**

const plot_style

**SEE ALSO**

plot, plot.style_linebr, plot.style_histogram, plot.style_cross, plot.style_area, plot.style_areabr, plot.style_columns, plot.style_circles, plot.style_stepline, plot.style_stepline_diamond, plot.style_steplinebr

---

### plot.style_linebr

A named constant for the 'Line With Breaks' style, to be used as an argument for the style parameter in the plot function. Similar to plot.style_line, except the gaps in the data are not filled.

**TYPE**

const plot_style

**SEE ALSO**

plot, plot.style_line, plot.style_histogram, plot.style_cross, plot.style_area, plot.style_areabr, plot.style_columns, plot.style_circles, plot.style_stepline, plot.style_stepline_diamond, plot.style_steplinebr

---

### plot.style_stepline

A named constant for the 'Step Line' style, to be used as an argument for the style parameter in the plot function.

**TYPE**

const plot_style

**SEE ALSO**

plot, plot.style_line, plot.style_linebr, plot.style_histogram, plot.style_cross, plot.style_area, plot.style_areabr, plot.style_columns, plot.style_circles, plot.style_stepline_diamond, plot.style_steplinebr

---

### plot.style_stepline_diamond

A named constant for the 'Step Line With Diamonds' style, to be used as an argument for the style parameter in the plot function. Similar to plot.style_stepline, except the data changes are also marked with the Diamond shapes.

**TYPE**

const plot_style

**SEE ALSO**

plot, plot.style_line, plot.style_linebr, plot.style_histogram, plot.style_cross, plot.style_area, plot.style_areabr, plot.style_columns, plot.style_circles, plot.style_stepline, plot.style_steplinebr

---

### plot.style_steplinebr

A named constant for the 'Step line with Breaks' style, to be used as an argument for the style parameter in the plot function.

**TYPE**

const plot_style

**SEE ALSO**

plot, plot.style_line, plot.style_linebr, plot.style_histogram, plot.style_cross, plot.style_area, plot.style_areabr, plot.style_columns, plot.style_circles, plot.style_stepline, plot.style_stepline_diamond

---

### position.bottom_center

Table position is used in table.new, table.cell functions.

Binds the table to the bottom edge in the center.

**TYPE**

const string

**SEE ALSO**

table.new, table.cell, table.set_position, position.top_left, position.top_center, position.top_right, position.middle_left, position.middle_center, position.middle_right, position.bottom_left, position.bottom_right

---

### position.bottom_left

Table position is used in table.new, table.cell functions.

Binds the table to the bottom left of the screen.

**TYPE**

const string

**SEE ALSO**

table.new, table.cell, table.set_position, position.top_left, position.top_center, position.top_right, position.middle_left, position.middle_center, position.middle_right, position.bottom_center, position.bottom_right

---

### position.bottom_right

Table position is used in table.new, table.cell functions.

Binds the table to the bottom right of the screen.

**TYPE**

const string

**SEE ALSO**

table.new, table.cell, table.set_position, position.top_left, position.top_center, position.top_right, position.middle_left, position.middle_center, position.middle_right, position.bottom_left, position.bottom_center

---

### position.middle_center

Table position is used in table.new, table.cell functions.

Binds the table to the center of the screen.

**TYPE**

const string

**SEE ALSO**

table.new, table.cell, table.set_position, position.top_left, position.top_center, position.top_right, position.middle_left, position.middle_right, position.bottom_left, position.bottom_center, position.bottom_right

---

### position.middle_left

Table position is used in table.new, table.cell functions.

Binds the table to the left side of the screen.

**TYPE**

const string

**SEE ALSO**

table.new, table.cell, table.set_position, position.top_left, position.top_center, position.top_right, position.middle_center, position.middle_right, position.bottom_left, position.bottom_center, position.bottom_right

---

### position.middle_right

Table position is used in table.new, table.cell functions.

Binds the table to the right side of the screen.

**TYPE**

const string

**SEE ALSO**

table.new, table.cell, table.set_position, position.top_left, position.top_center, position.top_right, position.middle_left, position.middle_center, position.bottom_left, position.bottom_center, position.bottom_right

---

### position.top_center

Table position is used in table.new, table.cell functions.

Binds the table to the top edge in the center.

**TYPE**

const string

**SEE ALSO**

table.new, table.cell, table.set_position, position.top_left, position.top_right, position.middle_left, position.middle_center, position.middle_right, position.bottom_left, position.bottom_center, position.bottom_right

---

### position.top_left

Table position is used in table.new, table.cell functions.

Binds the table to the upper-left edge.

**TYPE**

const string

**SEE ALSO**

table.new, table.cell, table.set_position, position.top_center, position.top_right, position.middle_left, position.middle_center, position.middle_right, position.bottom_left, position.bottom_center, position.bottom_right

---

### position.top_right

Table position is used in table.new, table.cell functions.

Binds the table to the upper-right edge.

**TYPE**

const string

**SEE ALSO**

table.new, table.cell, table.set_position, position.top_left, position.top_center, position.middle_left, position.middle_center, position.middle_right, position.bottom_left, position.bottom_center, position.bottom_right

---

### scale.left

Scale value for indicator function. Indicator is added to the left price scale.

**TYPE**

const scale_type

**SEE ALSO**

indicator

---

### scale.none

Scale value for indicator function. Indicator is added in 'No Scale' mode. Can be used only with 'overlay=true'.

**TYPE**

const scale_type

**SEE ALSO**

indicator

---

### scale.right

Scale value for indicator function. Indicator is added to the right price scale.

**TYPE**

const scale_type

**SEE ALSO**

indicator

---

### session.extended

Constant for extended session type (with extended hours data).

**TYPE**

const string

**SEE ALSO**

session.regular, syminfo.session

---

### session.regular

Constant for regular session type (no extended hours data).

**TYPE**

const string

**SEE ALSO**

session.extended, syminfo.session

---

### settlement_as_close.inherit

A constant to specify the value of the settlement_as_close parameter in ticker.new and ticker.modify functions.

**TYPE**

const settlement

**SEE ALSO**

ticker.new, ticker.modify, settlement_as_close.on, settlement_as_close.off

---

### settlement_as_close.off

A constant to specify the value of the settlement_as_close parameter in ticker.new and ticker.modify functions.

**TYPE**

const settlement

**SEE ALSO**

ticker.new, ticker.modify, settlement_as_close.on, settlement_as_close.inherit

---

### settlement_as_close.on

A constant to specify the value of the settlement_as_close parameter in ticker.new and ticker.modify functions.

**TYPE**

const settlement

**SEE ALSO**

ticker.new, ticker.modify, settlement_as_close.inherit, settlement_as_close.off

---

### shape.arrowdown

Shape style for plotshape function.

**TYPE**

const string

**SEE ALSO**

plotshape

---

### shape.arrowup

Shape style for plotshape function.

**TYPE**

const string

**SEE ALSO**

plotshape

---

### shape.circle

Shape style for plotshape function.

**TYPE**

const string

**SEE ALSO**

plotshape

---

### shape.cross

Shape style for plotshape function.

**TYPE**

const string

**SEE ALSO**

plotshape

---

### shape.diamond

Shape style for plotshape function.

**TYPE**

const string

**SEE ALSO**

plotshape

---

### shape.flag

Shape style for plotshape function.

**TYPE**

const string

**SEE ALSO**

plotshape

---

### shape.labeldown

Shape style for plotshape function.

**TYPE**

const string

**SEE ALSO**

plotshape

---

### shape.labelup

Shape style for plotshape function.

**TYPE**

const string

**SEE ALSO**

plotshape

---

### shape.square

Shape style for plotshape function.

**TYPE**

const string

**SEE ALSO**

plotshape

---

### shape.triangledown

Shape style for plotshape function.

**TYPE**

const string

**SEE ALSO**

plotshape

---

### shape.triangleup

Shape style for plotshape function.

**TYPE**

const string

**SEE ALSO**

plotshape

---

### shape.xcross

Shape style for plotshape function.

**TYPE**

const string

**SEE ALSO**

plotshape

---

### size.auto

A constant to specify the size of the graphics drawn by plotchar, plotshape, label.new, and box.new. Adjusts the size of the graphics automatically.

**TYPE**

const string

**SEE ALSO**

plotshape, plotchar, label.set_size, size.tiny, size.small, size.normal, size.large, size.huge

---

### size.huge

A constant to specify the size of the graphics drawn by plotchar, plotshape, label.new, box.new, and table.cell. Sets the size to huge.

**TYPE**

const string

**SEE ALSO**

plotshape, plotchar, label.set_size, size.auto, size.tiny, size.small, size.normal, size.large

---

### size.large

A constant to specify the size of the graphics drawn by plotchar, plotshape, label.new, box.new, and table.cell. Sets the size to large.

**TYPE**

const string

**SEE ALSO**

plotshape, plotchar, label.set_size, size.auto, size.tiny, size.small, size.normal, size.huge

---

### size.normal

A constant to specify the size of the graphics drawn by plotchar, plotshape, label.new, box.new, and table.cell. Sets the size to normal.

**TYPE**

const string

**SEE ALSO**

plotshape, plotchar, label.set_size, size.auto, size.tiny, size.small, size.large, size.huge

---

### size.small

A constant to specify the size of the graphics drawn by plotchar, plotshape, label.new, box.new, and table.cell. Sets the size to small.

**TYPE**

const string

**SEE ALSO**

plotshape, plotchar, label.set_size, size.auto, size.tiny, size.normal, size.large, size.huge

---

### size.tiny

A constant to specify the size of the graphics drawn by plotchar, plotshape, label.new, box.new, and table.cell. Sets the size to tiny.

**TYPE**

const string

**SEE ALSO**

plotshape, plotchar, label.set_size, size.auto, size.small, size.normal, size.large, size.huge

---

### splits.denominator

A named constant for the request.splits function. Is used to request the denominator (the number below the line in a fraction) of a splits.

**TYPE**

const string

**SEE ALSO**

request.splits

---

### splits.numerator

A named constant for the request.splits function. Is used to request the numerator (the number above the line in a fraction) of a splits.

**TYPE**

const string

**SEE ALSO**

request.splits

---

### strategy.cash

This is one of the arguments that can be supplied to the default_qty_type parameter in the strategy declaration statement. It is only relevant when no value is used for the ‘qty’ parameter in strategy.entry or strategy.order function calls. It specifies that an amount of cash in the strategy.account_currency will be used to enter trades.

**TYPE**

const string

**EXAMPLE**

```pine
//@version=6
strategy("strategy.cash", overlay = true, default_qty_value = 50, default_qty_type = strategy.cash, initial_capital = 1000000)

if bar_index == 0
    // As ‘qty’ is not defined, the previously defined values for the `default_qty_type` and `default_qty_value` parameters are used to enter trades, namely 50 units of cash in the currency of `strategy.account_currency`.
    // `qty` is calculated as (default_qty_value)/(close price). If current price is $5, then qty = 50/5 = 10.
    strategy.entry("EN", strategy.long)
if bar_index == 2
    strategy.close("EN")
```

**SEE ALSO**

strategy

---

### strategy.commission.cash_per_contract

Commission type for an order. Money displayed in the account currency per contract.

**TYPE**

const string

**SEE ALSO**

strategy

---

### strategy.commission.cash_per_order

Commission type for an order. Money displayed in the account currency per order.

**TYPE**

const string

**SEE ALSO**

strategy

---

### strategy.commission.percent

Commission type for an order. A percentage of the cash volume of order.

**TYPE**

const string

**SEE ALSO**

strategy

---

### strategy.direction.all

It allows strategy to open both long and short positions.

**TYPE**

const string

**SEE ALSO**

strategy.risk.allow_entry_in

---

### strategy.direction.long

It allows strategy to open only long positions.

**TYPE**

const string

**SEE ALSO**

strategy.risk.allow_entry_in

---

### strategy.direction.short

It allows strategy to open only short positions.

**TYPE**

const string

**SEE ALSO**

strategy.risk.allow_entry_in

---

### strategy.fixed

This is one of the arguments that can be supplied to the default_qty_type parameter in the strategy declaration statement. It is only relevant when no value is used for the ‘qty’ parameter in strategy.entry or strategy.order function calls. It specifies that a number of contracts/shares/lots will be used to enter trades.

**TYPE**

const string

**EXAMPLE**

```pine
//@version=6
strategy("strategy.fixed", overlay = true, default_qty_value = 50, default_qty_type = strategy.fixed, initial_capital = 1000000)

if bar_index == 0
    // As ‘qty’ is not defined, the previously defined values for the `default_qty_type` and `default_qty_value` parameters are used to enter trades, namely 50 contracts.
    // qty = 50
    strategy.entry("EN", strategy.long)
if bar_index == 2
    strategy.close("EN")
```

**SEE ALSO**

strategy

---

### strategy.long

A named constant for use with the direction parameter of the strategy.entry and strategy.order commands. It specifies that the command creates a buy order.

**TYPE**

const strategy_direction

**SEE ALSO**

strategy.entry, strategy.exit, strategy.order

---

### strategy.oca.cancel

A named constant for use with the oca_type parameter of the strategy.entry and strategy.order commands. It specifies that the strategy cancels the unfilled order when another order with the same oca_name and oca_type executes.

**TYPE**

const string

**REMARKS**

Strategies cannot cancel or reduce pending orders from an OCA group if they execute on the same tick. For example, if the market price triggers two stop orders from strategy.order calls with the same oca_* arguments, the strategy cannot fully or partially cancel either one.

**SEE ALSO**

strategy.entry, strategy.exit, strategy.order

---

### strategy.oca.none

A named constant for use with the oca_type parameter of the strategy.entry and strategy.order commands. It specifies that the order executes independently of all other orders, including those with the same oca_name.

**TYPE**

const string

**SEE ALSO**

strategy.entry, strategy.exit, strategy.order

---

### strategy.oca.reduce

A named constant for use with the oca_type parameter of the strategy.entry and strategy.order commands. It specifies that when another order with the same oca_name and oca_type executes, the strategy reduces the unfilled order by that order's size. If the unfilled order's size reaches 0 after reduction, it is the same as canceling the order entirely.

**TYPE**

const string

**REMARKS**

Strategies cannot cancel or reduce pending orders from an OCA group if they execute on the same tick. For example, if the market price triggers two stop orders from strategy.order calls with the same oca_* arguments, the strategy cannot fully or partially cancel either one.

Orders from strategy.exit automatically use this OCA type, and they belong to the same OCA group by default.

**SEE ALSO**

strategy.entry, strategy.exit, strategy.order

---

### strategy.percent_of_equity

This is one of the arguments that can be supplied to the default_qty_type parameter in the strategy declaration statement. It is only relevant when no value is used for the ‘qty’ parameter in strategy.entry or strategy.order function calls. It specifies that a percentage (0-100) of equity will be used to enter trades.

**TYPE**

const string

**EXAMPLE**

```pine
//@version=6
strategy("strategy.percent_of_equity", overlay = false, default_qty_value = 100, default_qty_type = strategy.percent_of_equity, initial_capital = 1000000)

// As ‘qty’ is not defined, the previously defined values for the `default_qty_type` and `default_qty_value` parameters are used to enter trades, namely 100% of available equity.
if bar_index == 0
    strategy.entry("EN", strategy.long)
if bar_index == 2
    strategy.close("EN")
plot(strategy.equity)

 // The ‘qty’ parameter is set to 10. Entering position with fixed size of 10 contracts and entry market price = (10 * close).
if bar_index == 4
    strategy.entry("EN", strategy.long, qty = 10)
if bar_index == 6
    strategy.close("EN")
```

**SEE ALSO**

strategy

---

### strategy.short

A named constant for use with the direction parameter of the strategy.entry and strategy.order commands. It specifies that the command creates a sell order.

**TYPE**

const strategy_direction

**SEE ALSO**

strategy.entry, strategy.exit, strategy.order

---

### text.align_bottom

Vertical text alignment for box.new, box.set_text_valign, table.cell and table.cell_set_text_valign functions.

**TYPE**

const string

**SEE ALSO**

table.cell, table.cell_set_text_valign, text.align_center, text.align_left, text.align_right

---

### text.align_center

Text alignment for box.new, box.set_text_halign, box.set_text_valign, label.new and label.set_textalign functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, text.align_left, text.align_right

---

### text.align_left

Horizontal text alignment for box.new, box.set_text_halign, label.new and label.set_textalign functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, text.align_center, text.align_right

---

### text.align_right

Horizontal text alignment for box.new, box.set_text_halign, label.new and label.set_textalign functions.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_style, text.align_center, text.align_left

---

### text.align_top

Vertical text alignment for box.new, box.set_text_valign, table.cell and table.cell_set_text_valign functions.

**TYPE**

const string

**SEE ALSO**

table.cell, table.cell_set_text_valign, text.align_center, text.align_left, text.align_right

---

### text.format_bold

A named constant for use with the text_formatting parameter of the label.new(), box.new(), table.cell(), and *set_text_formatting() functions. Makes the text bold.

**TYPE**

const text_format

**SEE ALSO**

label.new, box.new, table.cell

---

### text.format_italic

A named constant for use with the text_formatting parameter of the label.new(), box.new(), table.cell(), and *set_text_formatting() functions. Italicizes the text.

**TYPE**

const text_format

**SEE ALSO**

label.new, box.new, table.cell

---

### text.format_none

A named constant for use with the text_formatting parameter of the label.new(), box.new(), table.cell(), and *set_text_formatting() functions. Signifies no special text formatting.

**TYPE**

const text_format

**SEE ALSO**

label.new, box.new, table.cell

---

### text.wrap_auto

Automatic wrapping mode for box.new and box.set_text_wrap functions.

**TYPE**

const string

**SEE ALSO**

box.new, box.set_text, box.set_text_wrap

---

### text.wrap_none

Disabled wrapping mode for box.new and box.set_text_wrap functions.

**TYPE**

const string

**SEE ALSO**

box.new, box.set_text, box.set_text_wrap

---

### true

Literal representing one of the values a bool variable can hold, or an expression can evaluate to when it uses comparison or logical operators.

**REMARKS**

See the User Manual for comparison operators and logical operators.

**SEE ALSO**

bool

---

### xloc.bar_index

A constant that specifies how functions that create and modify Pine drawings interpret x-coordinates. If xloc = xloc.bar_index, the drawing object treats each x-coordinate as a bar_index value.

**TYPE**

const string

**SEE ALSO**

xloc.bar_time, line.new, label.new, box.new, polyline.new, line.set_xloc, label.set_xloc

---

### xloc.bar_time

A constant that specifies how functions that create and modify Pine drawings interpret x-coordinates. If xloc = xloc.bar_time, the drawing object treats each x-coordinate as a UNIX timestamp, expressed in milliseconds.

**TYPE**

const string

**SEE ALSO**

xloc.bar_index, line.new, label.new, box.new, polyline.new, line.set_xloc, label.set_xloc, xloc.bar_index

---

### yloc.abovebar

A named constant that specifies the algorithm of interpretation of y-value in function label.new.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_yloc, yloc.price, yloc.belowbar

---

### yloc.belowbar

A named constant that specifies the algorithm of interpretation of y-value in function label.new.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_yloc, yloc.price, yloc.abovebar

---

### yloc.price

A named constant that specifies the algorithm of interpretation of y-value in function label.new.

**TYPE**

const string

**SEE ALSO**

label.new, label.set_yloc, yloc.abovebar, yloc.belowbar
