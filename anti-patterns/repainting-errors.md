# 重绘错误反例

重绘是 Pine Script 中最常见且最难发现的问题之一。以下是最容易导致重绘的错误模式。

## 1. request.security() 未来泄漏

### ❌ 错误示例：直接使用实时数据
```pine
//@version=6
indicator("错误：未来泄漏", overlay=true)

// ❌ 危险：会获取未完成的日线数据
dailyClose = request.security(syminfo.tickerid, "D", close)

// 在当前K线显示明天的日线数据
plot(dailyClose, "日线收盘", color.red, 2)

// 基于未来数据的信号
buySignal = close > dailyClose
plotshape(buySignal, style=shape.triangleup, location=location.belowbar)
```

### 🚨 问题说明
- `request.security()` 默认会返回当前周期的实时数据
- 日线在完成前会不断变化，导致"未来数据"泄漏到当前
- 信号在实时K线上会不断变化，历史表现看起来完美但实际不可行

### ✅ 正确做法：使用偏移
```pine
//@version=6
indicator("正确：避免未来泄漏", overlay=true)

// ✅ 安全：使用已确认的日线数据
dailyClose = request.security(
    syminfo.tickerid,
    "D",
    close[1],  // 使用前一根已确认的日线
    lookahead=barmerge.lookahead_on  // 明确设置lookahead
)

// 仅显示已确认的数据
plot(dailyClose, "日线收盘", color.blue, 2)

// 基于历史数据的信号
buySignal = close > dailyClose
plotshape(buySignal, style=shape.triangleup, location=location.belowbar)
```

## 2. 实时K线上的信号重绘

### ❌ 错误示例：使用实时数据生成信号
```pine
//@version=6
indicator("错误：实时信号重绘")

// ❌ 使用实时close值（会在实时K线上变化）
rsi = ta.rsi(close, 14)
oversoldSignal = ta.crossunder(rsi, 30)

// 信号会在实时K线上反复出现和消失
plotshape(oversoldSignal, "超卖信号",
          style=shape.labelup, location=location.belowbar)

// 基于实时信号的入场标记
if oversoldSignal
    label.new(bar_index, low, "买入", color.green)
```

### 🚨 问题说明
- `close` 在实时K线上会不断变化
- RSI值会随之变化，导致信号反复触发
- 标签会随着信号出现和消失，造成混乱

### ✅ 正确做法：等待K线确认
```pine
//@version=6
indicator("正确：确认信号")

// ✅ 使用barstate.isconfirmed确保K线完成
rsi = ta.rsi(close, 14)
oversoldSignal = ta.crossunder(rsi[1], 30) and barstate.isconfirmed

// 信号只会在K线收盘时触发一次
plotshape(oversoldSignal, "超卖信号",
          style=shape.labelup, location=location.belowbar)

// 使用var避免标签重绘
var label buyLabel = na
if oversoldSignal
    if na(buyLabel)
        buyLabel := label.new(bar_index, low, "买入", color.green)
else
    if not na(buyLabel)
        label.delete(buyLabel)
        buyLabel := na
```

## 3. 动态支撑阻力重绘

### ❌ 错误示例：动态调整历史水平
```pine
//@version=6
indicator("错误：动态支撑阻力", overlay=true)

// ❌ 使用pivot点但允许历史调整
leftLen = input.int(10, "左侧长度")
rightLen = input.int(10, "右侧长度")

// pivot.high允许未来数据影响历史pivot
pivothigh = ta.pivothigh(high, leftLen, rightLen)

// 历史pivot会随着新K线而移动
plot(pivothigh, "阻力", color.red)
```

### 🚨 问题说明
- `ta.pivothigh` 默认允许未来数据调整历史pivot点
- 当新K线出现时，过去的pivot点可能改变位置
- 导致回测结果与实际交易不符

### ✅ 正确做法：固定历史pivot
```pine
//@version=6
indicator("正确：固定支撑阻力", overlay=true)

// ✅ 使用var固定历史pivot
var float resistanceLevel = na
var float supportLevel = na
var int lastPivotBar = na

// 检测新的pivot点（只确认）
ph = ta.pivothigh(high, 10, 10)
pl = ta.pivotlow(low, 10, 10)

// 只在确认后更新（不改变历史）
if not na(ph)
    resistanceLevel := ph
    lastPivotBar := bar_index

if not na(pl)
    supportLevel := pl
    lastPivotBar := bar_index

// 绘制固定的水平线
plot(resistanceLevel, "阻力", color.red, style=plot.style_linebr)
plot(supportLevel, "支撑", color.green, style=plot.style_linebr)
```

## 4. 计算时使用未来数据

### ❌ 错误示例：在实时K线上使用未来值
```pine
//@version=6
indicator("错误：未来计算")

// ❌ 在实时K线上使用最高最低价
atr = ta.atr(14)
upperBand = high + atr
lowerBand = low - atr

// 实时K线的high/low会变化
plot(upperBand, "上轨", color.red)
plot(lowerBand, "下轨", color.green)

// 基于未来值的突破信号
breakout = ta.crossover(close, upperBand)
plotshape(breakout, "突破", style=shape.triangleup)
```

### 🚨 问题说明
- `high` 和 `low` 在实时K线上会不断更新
- 基于这些值绘制的通道会实时变化
- 突破信号可能在K线收盘前触发然后消失

### ✅ 正确做法：使用确认值
```pine
//@version=6
indicator("正确：确认值计算")

// ✅ 使用前一根K线的确认值
prevHigh = high[1]
prevLow = low[1]
prevAtr = ta.atr(14)[1]

// 计算固定通道
upperBand = prevHigh + prevAtr
lowerBand = prevLow - prevAtr

// 通道值在当前K线固定
plot(upperBand, "上轨", color.red)
plot(lowerBand, "下轨", color.green)

// 突破信号基于固定值
breakout = ta.crossover(close, upperBand)
plotshape(breakout, "突破", style=shape.triangleup)
```

## 5. 多时间框架重绘

### ❌ 错误示例：混合时间框架导致不一致
```pine
//@version=6
indicator("错误：MTF重绘", overlay=true)

// ❌ 获取不同时间框架的数据但未同步
m5_close = request.security(syminfo.tickerid, "5", close)
h1_close = request.security(syminfo.tickerid, "60", close)

// 不同时间框架的数据更新频率不同
// 导致指标在不同时间不一致
alignment = m5_close > h1_close
bgcolor(alignment ? color.green : color.red, transp=90)

// 基于对齐信号的交易
plotshape(alignment, "对齐信号", style=shape.circle)
```

### 🚨 问题说明
- 不同时间框架的数据更新频率不同
- 5分钟数据每5分钟更新，1小时数据每小时更新
- 会导致背景色在大部分时间为na或错误

### ✅ 正确做法：同步更新
```pine
//@version=6
indicator("正确：MTF同步", overlay=true)

// ✅ 缓存高时间框架数据
var float h1_close = na
var int lastHour = na

// 只在小时变化时更新
currentHour = hour(time)
if currentHour != lastHour
    h1_close := request.security(
        syminfo.tickerid,
        "60",
        close[1],
        lookahead=barmerge.lookahead_on
    )
    lastHour := currentHour

// 使用当前周期的5分钟数据
m5_close = close

// 两个值都是确认值
alignment = m5_close > h1_close
bgcolor(not na(alignment) ?
        (alignment ? color.green : color.red) : na,
        transp=90)

plotshape(alignment, "对齐信号", style=shape.circle)
```

## 6. 循环引用导致重绘

### ❌ 错误示例：循环依赖
```pine
//@version=6
indicator("错误：循环引用")

// ❌ value依赖自身的历史值
// 但在实时K线上会循环更新
var float value = 0
value := ta.sma(value, 10) + close * 0.1

// 在实时K线上，value会不断重绘
plot(value, "循环值", color.red)
```

### 🚨 问题说明
- `value` 依赖于自身的平滑值
- 在实时K线上，每次更新都会影响后续计算
- 导致无限循环式的重绘

### ✅ 正确做法：明确计算链
```pine
//@version=6
indicator("正确：明确计算")

// ✅ 使用独立的计算链
rawValue = close * 0.1
var float[] rawHistory = array.new<float>(10, 0)

// 只在K线确认时更新
if barstate.isconfirmed
    array.unshift(rawHistory, rawValue)
    if array.size(rawHistory) > 10
        array.pop(rawHistory)

// 计算基于历史数据
smoothValue = array.avg(rawHistory)
plot(smoothValue, "平滑值", color.blue)
```

## 7. timenow 使用错误

### ❌ 错误示例：使用当前时间
```pine
//@version=6
indicator("错误：timenow使用")

// ❌ timenow在实时K线上不断变化
isSessionEnd = hour(timenow) >= 15 and minute(timenow) >= 30

// 判断会随实时时间变化
bgcolor(isSessionEnd ? color.red : na)

// 基于时间的信号
if isSessionEnd
    label.new(bar_index, high, "收盘时间", color.red)
```

### 🚨 问题说明
- `timenow` 是脚本运行的实时时间
- 在实时K线上会不断变化
- 历史K线上的判断也会随着时间推移而改变

### ✅ 正确做法：使用K线时间
```pine
//@version=6
indicator("正确：K线时间")

// ✅ 使用K线自己的时间
isSessionEnd = hour(time) >= 15 and minute(time) >= 30

// 判断基于K线时间，固定不变
bgcolor(isSessionEnd ? color.green : na)

// 只在最后一根K线显示实时信息
if barstate.islast
    label.new(bar_index, high,
              "当前时间: " + str.format("{0,time,HH:mm}", timenow),
              color.blue)
```

## 检查重绘的清单

1. **是否使用 request.security() 而没有偏移？**
2. **是否在实时K线上使用 close/high/low？**
3. **是否等待 barstate.isconfirmed？**
4. **是否使用 timenow 进行历史判断？**
5. **是否有循环依赖的变量？**
6. **是否混合不同更新频率的数据？**

## 避免重绘的黄金法则

1. **总是使用偏移**：`value[1]` 是你的朋友
2. **等待确认**：`barstate.isconfirmed` 是安全锁
3. **固定历史**：历史数据不应该改变
4. **避免 timenow**：除非只用于最后一根K线
5. **明确 lookahead**：清楚了解 request.security 的行为

记住：**如果回测结果看起来太美好，很可能存在重绘问题！**