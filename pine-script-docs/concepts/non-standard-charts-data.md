# Concepts / Non-standard charts data

> Source: https://www.tradingview.com/pine-script-docs/concepts/non-standard-charts-data/
> Retrieved at: 2025-10-12T12:18:56.113Z

# Non-standard charts data

## Introduction

Pine Script® features several `ticker.*()` functions that generate *ticker identifiers* for requesting data from *non-standard* chart feeds. The available functions that create these ticker IDs are [ticker.heikinashi()](https://www.tradingview.com/pine-script-reference/v6/#fun_ticker.heikinashi), [ticker.renko()](https://www.tradingview.com/pine-script-reference/v6/#fun_ticker.renko), [ticker.linebreak()](https://www.tradingview.com/pine-script-reference/v6/#fun_ticker.linebreak), [ticker.kagi()](https://www.tradingview.com/pine-script-reference/v6/#fun_ticker.kagi), and [ticker.pointfigure()](https://www.tradingview.com/pine-script-reference/v6/#fun_ticker.pointfigure). Scripts can use these functions’ returned values as the `symbol` argument in [request.security()](https://www.tradingview.com/pine-script-reference/v6/#fun_request.security) calls to access non-standard chart data while running on *any* chart type.

NoticeIt’s important to note that on TradingView, the [Renko](https://www.tradingview.com/support/solutions/43000502284), [Line Break](https://www.tradingview.com/support/solutions/43000502273), [Kagi](https://www.tradingview.com/support/solutions/43000502272), and [Point & Figure](https://www.tradingview.com/support/solutions/43000502276) chart types construct bars using price data from *lower timeframes*. Therefore, these chart types only *approximate* the values that would occur if they used tick data.

## ​ticker.heikinashi()​

*Heikin-Ashi* means *average bar* in Japanese. The open/high/low/close values of Heikin-Ashi candlesticks are synthetic; they are not actual market prices. They are calculated by averaging combinations of real OHLC values from the current and previous bar. The calculations used make Heikin-Ashi bars less noisy than normal candlesticks. They can be useful to make visual assessments, but are unsuited to backtesting or automated trading, as orders execute on market prices — not Heikin-Ashi prices.

The [ticker.heikinashi()](https://www.tradingview.com/pine-script-reference/v6/#fun_ticker%7Bdot%7Dheikinashi) function creates a special ticker identifier for requesting Heikin-Ashi data with the [request.security()](https://www.tradingview.com/pine-script-reference/v6/#fun_request%7Bdot%7Dsecurity) function.

This script requests the close value of Heikin-Ashi bars and plots them on top of the normal candlesticks:

![image](https://www.tradingview.com/pine-script-docs/_astro/NonStandardCharts-TickerHeikinAshi-01.Cf57zbCt_1Ykjzf.webp)

[Pine Script®](https://tradingview.com/pine-script-docs)

```pine
//@version=6
indicator("HA Close", "", true)
haTicker = ticker.heikinashi(syminfo.tickerid)
haClose = request.security(haTicker, timeframe.period, close)
plot(haClose, "HA Close", color.black, 3)
```

Note that:

-   The close values for Heikin-Ashi bars plotted as the black line are very different from those of real candles using market prices. They act more like a moving average.
-   The black line appears over the chart bars because we have selected “Visual Order/Bring to Front” from the script’s “More” menu.

If you wanted to omit values for extended hours in the last example, an intermediary ticker without extended session information would need to be created first:

![image](https://www.tradingview.com/pine-script-docs/_astro/NonStandardCharts-TickerHeikinAshi-02.B9TEp43B_ZjVqEN.webp)

[Pine Script®](https://tradingview.com/pine-script-docs)

```pine
//@version=6
indicator("HA Close", "", true)
regularSessionTicker = ticker.new(syminfo.prefix, syminfo.ticker, session.regular)
haTicker = ticker.heikinashi(regularSessionTicker)
haClose = request.security(haTicker, timeframe.period, close, gaps = barmerge.gaps_on)
plot(haClose, "HA Close", color.black, 3, plot.style_linebr)
```

Note that:

-   We use the [ticker.new()](https://www.tradingview.com/pine-script-reference/v6/#fun_ticker%7Bdot%7Dnew) function first, to create a ticker without extended session information.
-   We use that ticker instead of [syminfo.tickerid](https://www.tradingview.com/pine-script-reference/v6/#var_syminfo%7Bdot%7Dtickerid) in our [ticker.heikinashi()](https://www.tradingview.com/pine-script-reference/v6/#fun_ticker%7Bdot%7Dheikinashi) call.
-   In our [request.security()](https://www.tradingview.com/pine-script-reference/v6/#fun_request%7Bdot%7Dsecurity) call, we set the `gaps` parameter’s value to `barmerge.gaps_on`. This instructs the function not to use previous values to fill slots where data is absent. This makes it possible for it to return [na](https://www.tradingview.com/pine-script-reference/v6/#var_na) values outside of regular sessions.
-   To be able to see this on the chart, we also need to use a special `plot.style_linebr` style, which breaks the plots on [na](https://www.tradingview.com/pine-script-reference/v6/#var_na) values.

This script plots Heikin-Ashi candles under the chart:

![image](https://www.tradingview.com/pine-script-docs/_astro/NonStandardCharts-TickerHeikinAshi-03.DDXVmouO_ZyQNBR.webp)

[Pine Script®](https://tradingview.com/pine-script-docs)

```pine
//@version=6
indicator("Heikin-Ashi candles")
CANDLE_GREEN = #26A69A
CANDLE_RED   = #EF5350

haTicker = ticker.heikinashi(syminfo.tickerid)
[haO, haH, haL, haC] = request.security(haTicker, timeframe.period, [open, high, low, close])
candleColor = haC >= haO ? CANDLE_GREEN : CANDLE_RED
plotcandle(haO, haH, haL, haC, color = candleColor)
```

Note that:

-   We use a [tuple](https://www.tradingview.com/pine-script-docs/language/variable-declarations/#tuple-declarations) with [request.security()](https://www.tradingview.com/pine-script-reference/v6/#fun_request%7Bdot%7Dsecurity) to fetch four values with the same call.
-   We use [plotcandle()](https://www.tradingview.com/pine-script-reference/v6/#fun_plotcandle) to plot our candles. See the [Bar plotting](https://www.tradingview.com/pine-script-docs/visuals/bar-plotting/) page for more information.

## ​ticker.renko()​

*Renko* bars only plot price movements, without taking time or volume into consideration. They look like bricks stacked in adjacent columns. A new brick is only drawn after the price passes the top or bottom by a predetermined amount. The [ticker.renko()](https://www.tradingview.com/pine-script-reference/v6/#fun_ticker%7Bdot%7Drenko) function creates a ticker id which can be used with [request.security()](https://www.tradingview.com/pine-script-reference/v6/#fun_request%7Bdot%7Dsecurity) to fetch Renko values, but there is no Pine Script function to draw Renko bars on the chart:

[Pine Script®](https://tradingview.com/pine-script-docs)

```pine
//@version=6
indicator("", "", true)
renkoTicker = ticker.renko(syminfo.tickerid, "ATR", 10)
renkoLow = request.security(renkoTicker, timeframe.period, low)
plot(renkoLow)
```

## ​ticker.linebreak()​

The *Line Break* chart type displays a series of vertical boxes that are based on price changes. The [ticker.linebreak()](https://www.tradingview.com/pine-script-reference/v6/#fun_ticker%7Bdot%7Dlinebreak) function creates a ticker id which can be used with [request.security()](https://www.tradingview.com/pine-script-reference/v6/#fun_request%7Bdot%7Dsecurity) to fetch “Line Break” values, but there is no Pine Script function to draw such bars on the chart:

[Pine Script®](https://tradingview.com/pine-script-docs)

```pine
//@version=6
indicator("", "", true)
lineBreakTicker = ticker.linebreak(syminfo.tickerid, 3)
lineBreakClose = request.security(lineBreakTicker, timeframe.period, close)
plot(lineBreakClose)
```

## ​ticker.kagi()​

*Kagi* charts are made of a continuous line that changes directions. The direction changes when the price changes beyond a predetermined amount. The [ticker.kagi()](https://www.tradingview.com/pine-script-reference/v6/#fun_ticker%7Bdot%7Dkagi) function creates a ticker id which can be used with [request.security()](https://www.tradingview.com/pine-script-reference/v6/#fun_request%7Bdot%7Dsecurity) to fetch “Kagi” values, but there is no Pine Script function to draw such bars on the chart:

[Pine Script®](https://tradingview.com/pine-script-docs)

```pine
//@version=6
indicator("", "", true)
kagiBreakTicker = ticker.linebreak(syminfo.tickerid, 3)
kagiBreakClose = request.security(kagiBreakTicker, timeframe.period, close)
plot(kagiBreakClose)
```

## ​ticker.pointfigure()​

*Point and Figure* (PnF) charts only plot price movements, without taking time into consideration. A column of X’s is plotted as the price rises, and O’s are plotted when price drops. The [ticker.pointfigure()](https://www.tradingview.com/pine-script-reference/v6/#fun_ticker%7Bdot%7Dpointfigure) function creates a ticker id which can be used with [request.security()](https://www.tradingview.com/pine-script-reference/v6/#fun_request%7Bdot%7Dsecurity) to fetch “PnF” values, but there is no Pine Script function to draw such bars on the chart. Every column of X’s or O’s is represented with four numbers. You may think of them as synthetic OHLC PnF values:

[Pine Script®](https://tradingview.com/pine-script-docs)

```pine
//@version=6
indicator("", "", true)
pnfTicker = ticker.pointfigure(syminfo.tickerid, "hl", "ATR", 14, 3)
[pnfO, pnfC] = request.security(pnfTicker, timeframe.period, [open, close], barmerge.gaps_on)
plot(pnfO, "PnF Open", color.green, 4, plot.style_linebr)
plot(pnfC, "PnF Close", color.red, 4, plot.style_linebr)
```
