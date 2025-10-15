# 跨周期数据请求决策树

## 📊 起始问题：我需要从其他时间框架获取数据吗？

```
┌─────────────────────────────────────────────────────┐
│   ⏰ 跨周期数据：request.security() 使用指南         │
│   • 高时间框架分析 • 低时间框架细节 • 多周期确认     │
└─────────────────────────────────────────────────────┘
    │
    └─ 🎯 为什么需要跨周期数据？
        │
        ├─ 需要更高时间框架的趋势方向
        │   └─ ➡️ **趋势过滤**
        │
        ├─ 需要更低时间框架的精确入场
        │   └─ ➡️ **精确时机**
        │
        ├─ 需要多周期确认信号
        │   └─ ➡️ **信号确认**
        │
        └─ 需要不同周期的指标值
            └─ ➡️ **指标对比**
```

## 📈 高时间框架数据获取

```
┌─ 需求：获取高时间框架数据（如日线、周线）
│
├─ 🔧 基础语法
│   │
│   └─ ```pine
│       data = request.security(
│           symbol,        // 交易品种
│           timeframe,     // 目标时间框架
│           expression,    // 要获取的数据
│           gaps,          // 缺失数据处理
│           lookahead      // 未来数据处理
│       )
│       ```
│
├─ 📊 常用场景
│   │
│   ├─ 趋势方向判断
│   │   ```pine
│   │   // 获取日线MA判断大趋势
│   │   dailyMA200 = request.security(
│   │       syminfo.tickerid,
│   │       "1D",
│   │       ta.sma(close, 20)
│   │   )
│   │
│   │   // 只在大趋势向上时做多
│   │   buySignal = close > ta.sma(close, 20) and close > dailyMA200
│   │   ```
│   │
│   ├─ 关键价格水平
│   │   ```pine
│   │   // 获取日线支撑阻力
│   │   dailyHigh = request.security(
│   │       syminfo.tickerid, "1D", high
│   │   )
│   │   dailyLow = request.security(
│   │       syminfo.tickerid, "1D", low
│   │   )
│   │
│   │   plot(dailyHigh, "日高", color.red)
│   │   plot(dailyLow, "日低", color.green)
│   │   ```
│   │
│   └─ 指标确认
│       ```pine
│       // 获取日线RSI
│       dailyRSI = request.security(
│           syminfo.tickerid, "1D",
│           ta.rsi(close, 14)
│       )

│       // 多周期信号确认
│       m5Buy = ta.rsi(close, 14) < 30
│       d1TrendUp = dailyRSI > 50
│       finalBuy = m5Buy and d1TrendUp
│       ```
│
├─ ⚠️ 安全使用要点
│   │
│   ├─ 避免未来泄漏
│   │   ```pine
│   │   // ❌ 危险：可能未来泄漏
│   │   dailyClose = request.security(
│   │       syminfo.tickerid, "1D", close
│   │   )

│   │   // ✅ 安全：使用偏移
│   │   dailyClose = request.security(
│   │       syminfo.tickerid, "1D",
│   │       close[1],
│   │       lookahead=barmerge.lookahead_on
│   │   )
│   │   ```
│   │
│   ├─ 处理缺失数据
│   │   ```pine
│   │   // 处理数据缺失
│   │   weeklyData = request.security(
│   │       syminfo.tickerid, "W",
│   │       close,
│   │       gaps=barmerge.gaps_on,
│   │       lookahead=barmerge.lookahead_on
│   │   )
│   │
│   │   // 使用 nz() 处理 na 值
│   │   weeklyPrice = nz(weeklyData, close)
│   │   ```
│   │
│   └─ 缓存优化
│       ```pine
│       // 缓存高时间框架数据
│       var float dailyMA = na
│       if ta.change(time("D"))
│           dailyMA := request.security(
│               syminfo.tickerid, "1D",
│               ta.sma(close, 20)[1]
│           )
│       ```
│
└─ 🎯 最佳实践
    ├─ 使用 lookahead=barmerge.lookahead_on
    │   ```pine
    │   // 明确使用 lookahead
    │   data = request.security(..., lookahead=barmerge.lookahead_on)
    │   ```
    │
    ├─ 添加偏移保证安全
    │   ```pine
    │   // 添加 [1] 偏移
    │   safeData = request.security(..., close[1])
    │   ```
    │
    └─ 验证数据有效性
        ```pine
        // 检查数据有效性
        htfData = request.security(...)
        if not na(htfData)
            // 使用数据
        ```
```

## 📉 低时间框架数据获取

```
┌─ 需求：获取低时间框架数据（如秒级、tick级）
│
├─ 📊 使用场景
│   │
│   ├─ 精确入场时机
│   │   ```pine
│   │   // 在1分钟图表上获取15秒数据
│   │   sec15High = request.security(
│   │       syminfo.tickerid, "15S",
│   │       high,
│   │       gaps=barmerge.gaps_off,
│   │       lookahead=barmerge.lookahead_off
│   │   )

│   │   // 突破15秒高点入场
│   │   if ta.crossover(close, sec15High)
│   │       strategy.entry("Long", strategy.long)
│   │   ```
│   │
│   ├─ 微观结构分析
│   │   ```pine
│   │   // 获取tick数据（如果可用）
│   │   tickVolume = request.security(
│   │       syminfo.tickerid, "1S",
│   │       volume,
│   │       gaps=barmerge.gaps_off
│   │   )

│   │   // 分析短期成交量突增
│   │   volumeSpike = tickVolume > ta.sma(tickVolume, 10) * 3
│   │   ```
│   │
│   └─ 剥头皮策略
│       ```pine
│       // 快速进出策略
│       sec5Close = request.security(
│           syminfo.tickerid, "5S",
│           close[1]
│       )

│       // 快速均线交叉
│       sec5MA = ta.sma(sec5Close, 10)
│       if ta.crossover(sec5Close, sec5MA)
│           strategy.entry("Scalp", strategy.long)
│           strategy.exit("Exit", "Scalp", bars_after_entry=2)
│       ```
│
├─ ⚡ 性能优化
│   │
│   ├─ 减少请求频率
│   │   ```pine
│   │   // 只在需要时请求
│   │   var float lowTFData = na
│   │   if condition and barstate.isconfirmed
│   │       lowTFData := request.security(...)
│   │   ```
│   │
│   ├─ 使用 gaps=barmerge.gaps_off
│   │   ```pine
│   │   // 低时间框架数据通常有缺失
│   │   data = request.security(
│   │       ..., gaps=barmerge.gaps_off
│   │   )
│   │   ```
│   │
│   └─ 批量获取
│       ```pine
│       // 一次请求多个值
│       [high5, low5, close5] = request.security(
│           syminfo.tickerid, "5S",
│           [high, low, close]
│       )
│       ```
│
└─ ⚠️ 注意事项
    ├─ 数据可用性
    │   - 不是所有时间框架都可用
    │   - 取决于数据源
    │
    ├─ 计算负荷
    │   - 低时间框架数据量大
    │   - 可能影响性能
    │
    └─ 实时性
        - 低时间框架数据延迟更高
        - 考虑实际应用场景
```

## 🔄 多周期确认策略

```
┌─ 需求：多时间框架信号确认
│
├─ 📊 策略框架
│   └─ ```pine
│       //@version=6
│       strategy("多周期确认策略")
│
│       // 获取多个时间框架数据
│       h1_trend = request.security("1", "60", ta.ema(close, 50))
│       h4_trend = request.security("1", "240", ta.ema(close, 50))
│       d1_trend = request.security("1", "D", ta.ema(close, 50))
│
│       // 多周期趋势判断
│       trend_up = close > h1_trend and close > h4_trend and close > d1_trend
│       trend_down = close < h1_trend and close < h4_trend and close < d1_trend
│
│       // 当前周期信号
│       m5_signal = ta.rsi(close, 14) < 30
│
│       // 多周期确认
│       if m5_signal and trend_up
│           strategy.entry("Long", strategy.long)
│       ```
│
├─ 🎯 确认级别
│   │
│   ├─ 强确认（所有周期一致）
│   │   ```pine
│       // 三个周期全部看涨
│       strongBuy = m5_rsi < 30 and h1_rsi < 30 and h4_rsi < 30
│       ```
│   │
│   ├─ 中等确认（多数周期一致）
│   │   ```pine
│       // 两个周期看涨即可
│       mediumBuy = (m5_rsi < 30 and h1_rsi < 30) or
│                   (m5_rsi < 30 and h4_rsi < 30) or
│                   (h1_rsi < 30 and h4_rsi < 30)
│       ```
│   │
│   └─ 弱确认（高周期主导）
│       ```pine
│       // 只要高周期看涨
│       weakBuy = d1_trend_up and m5_signal
│       ```
│
├─ 📈 动态时间框架选择
│   └─ ```pine
│       // 根据波动率选择时间框架
│       atr = ta.atr(14)
│       volatility_level = atr / close * 100

│       // 高波动使用更长周期
│       htf_period = volatility_level > 2 ? "4H" : "1H"

│       htf_data = request.security(
│           syminfo.tickerid,
│           htf_period,
│           ta.sma(close, 20)
│       )
│       ```
│
└─ 💡 实用技巧
    ├─ 使用评分系统
    │   ```pine
    │   // 多周期评分
    │   score = 0
    │   if m5_condition => score += 1
    │   if h1_condition => score += 2
    │   if h4_condition => score += 3
    │   if d1_condition => score += 4

    │   // 根据评分决定
    │   if score >= 7
    │       strategy.entry(...)
    │   ```
    │
    ├─ 时间框架过滤器
    │   ```pine
    │   // 根据时间框架调整策略
    │   currentTF = timeframe.period
    │   isHigherTF = currentTF in ["60", "240", "D"]
    │
    │   if isHigherTF
    │       // 使用更宽松的条件
    │       threshold = 25
    │   else
    │       // 使用更严格的条件
    │       threshold = 20
    │   ```
    │
    └─ 渐进式确认
        ```pine
        // 逐步确认
        if m5_signal
            // 第一级：基础信号
            plotshape(1, "L1", style=shape.circle)

        if m5_signal and h1_confirm
            // 第二级：1小时确认
            plotshape(2, "L2", style=shape.square)

        if m5_signal and h1_confirm and h4_confirm
            // 第三级：4小时确认
            plotshape(3, "L3", style=shape.diamond)
        ```
```

## 📊 request.security() 参数详解

```
┌─ 参数详解
│
├─ symbol（交易品种）
│   │
│   ├─ 使用当前品种
│   │   ```pine
│   │   syminfo.tickerid
│   │   ```
│   │
│   ├─ 指定其他品种
│   │   ```pine
│   │   "NASDAQ:AAPL"
│   │   "BINANCE:BTCUSDT"
│   │   ```
│   │
│   └─ 动态品种
│       ```pine
│       // 根据输入选择品种
│       sym = input.symbol("NASDAQ:TSLA")
│       data = request.security(sym, "D", close)
│       ```
│
├─ timeframe（时间框架）
│   │
│   ├─ 预定义时间框架
│   │   ```pine
│   │   "1", "5", "15", "30", "60", "240", "D", "W", "M"
│   │   ```
│   │
│   ├─ 自定义时间框架
│   │   ```pine
│   │   "120"     // 2小时
│   │   "720"     // 12小时
│   │   "3D"      // 3天
│   │   "2W"      // 2周
│   │   ```
│   │
│   └─ 相对时间框架
│       ```pine
│       // 当前时间框架的倍数
│       multiplier = 4
│       htfTimeframe = str.tostring(timeframe.multiplier * multiplier)
│       ```
│
├─ expression（数据表达式）
│   │
│   ├─ 基础数据
│   │   ```pine
│   │   close, high, low, open, volume
│   │   ```
│   │
│   ├─ 指标计算
│   │   ```pine
│   │   ta.sma(close, 20)
│   │   ta.rsi(close, 14)
│   │   ta.macd(close, 12, 26, 9)
│   │   ```
│   │
│   ├─ 复合表达式
│   │   ```pine
│   │   ta.sma(close, 20) > ta.sma(close, 50)
│   │   ta.rsi(close, 14) > 50
│   │   ```
│   │
│   └─ 多值返回
│       ```pine
│       [ma20, ma50] = request.security(
│           syminfo.tickerid, "D",
│           [ta.sma(close, 20), ta.sma(close, 50)]
│       )
│       ```
│
├─ gaps（缺失数据处理）
│   │
│   ├─ barmerge.gaps_on
│   │   - 返回 na 值
│   │   - 适合需要知道数据缺失的场景
│   │
│   ├─ barmerge.gaps_off
│   │   - 返回最后一个有效值
│   │   - 适合连续数据
│   │
│   └─ 选择建议
│       ```pine
│       // 高时间框架数据用 gaps_on
│       dailyData = request.security(..., gaps=barmerge.gaps_on)

│       // 低时间框架数据用 gaps_off
│       tickData = request.security(..., gaps=barmerge.gaps_off)
│       ```
│
└─ lookahead（未来数据处理）
    │
    ├─ barmerge.lookahead_on
    │   - 允许访问未来数据（当前周期未完成的数据）
    │   - 可能导致重绘
    │
    ├─ barmerge.lookahead_off
    │   - 只访问已确认数据
    │   - 避免重绘
    │
    └─ 安全建议
        ```pine
        // 大多数情况使用 lookahead_on + 偏移
        data = request.security(
            syminfo.tickerid, "D",
            close[1],
            lookahead=barmerge.lookahead_on
        )

        // 需要绝对避免重绘时
        data = request.security(
            syminfo.tickerid, "D",
            close,
            lookahead=barmerge.lookahead_off
        )
        ```
```

## ⚠️ 常见问题和解决方案

### 问题1：重绘问题
```pine
// ❌ 导致重绘
dailyClose = request.security(syminfo.tickerid, "D", close)

// ✅ 解决方案1：使用偏移
dailyClose = request.security(syminfo.tickerid, "D", close[1])

// ✅ 解决方案2：使用 lookahead_off
dailyClose = request.security(
    syminfo.tickerid, "D",
    close,
    lookahead=barmerge.lookahead_off
)
```

### 问题2：性能问题
```pine
// ❌ 每次都请求
if condition
    data = request.security(...)

// ✅ 缓存数据
var float cachedData = na
if ta.change(time("D"))  // 每天更新一次
    cachedData := request.security(...)
```

### 问题3：数据不连续
```pine
// ❌ 直接使用可能导致错误
weeklyData = request.security(...)

// ✅ 处理 na 值
weeklyData = request.security(..., gaps=barmerge.gaps_on)
cleanData = nz(weeklyData, defaultValue)
```

### 问题4：时间框架不匹配
```pine
// ❌ 在非标准时间框架可能失败
data = request.security(syminfo.tickerid, "45", close)

// ✅ 使用标准时间框架
data = request.security(syminfo.tickerid, "60", close)
```

## 📋 最佳实践总结

1. **总是考虑重绘风险**
   - 优先使用偏移 [1]
   - 明确设置 lookahead 参数

2. **优化性能**
   - 缓存高时间框架数据
   - 减少不必要的请求
   - 批量获取多个值

3. **处理数据质量**
   - 检查 na 值
   - 设置合适的 gaps 参数
   - 验证数据有效性

4. **设计合理的策略**
   - 不要过度依赖高时间框架
   - 考虑数据延迟
   - 平衡复杂性和效果

5. **测试和验证**
   - 在历史数据上测试
   - 观察实时表现
   - 注意不同市场的差异

## 💡 快速参考表

| 场景 | 推荐参数设置 |
|------|-------------|
| 趋势过滤 | `close[1]`, `lookahead_on`, `gaps_on` |
| 精确入场 | `close`, `lookahead_off`, `gaps_off` |
| 指标对比 | `ta.indicator()[1]`, `lookahead_on` |
| 数据缓存 | 使用 `var` 变量存储 |
| 多品种 | 指定完整symbol路径 |

记住：**跨周期数据强大但需要谨慎使用，始终考虑重绘风险和性能影响**。