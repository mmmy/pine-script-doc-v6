# 警报实现决策树

## 🔔 起始问题：我需要实现什么类型的警报？

```
┌─────────────────────────────────────────────────────┐
│   ⚠️ Pine Script 警报类型选择                        │
│   • alertcondition() - UI条件警报                    │
│   • alert() - 动态消息警报                          │
│   • 策略订单填充警报                               │
└─────────────────────────────────────────────────────┘
    │
    └─ 📋 警报需求？
        │
        ├─ 简单条件触发（用户在UI中选择）
        │   └─ ➡️ **alertcondition()**
        │
        ├─ 复杂动态消息
        │   └─ ➡️ **alert()**
        │
        ├─ 策略交易信号
        │   └─ ➡️ **订单填充警报**
        │
        └─ 多种警报组合
            └─ ➡️ **混合方案**
```

## 📊 alertcondition() - UI条件警报

```
┌─ 选择：alertcondition()
│
├─ ✅ 适用场景
│   │
│   ├─ 简单买入/卖出信号
│   │   ```pine
│   │   // 交叉信号
│   │   [macdLine, signalLine] = ta.macd(close, 12, 26, 9)
│   │   bullishCross = ta.crossover(macdLine, signalLine)
│   │   bearishCross = ta.crossunder(macdLine, signalLine)
│   │
│   │   // 创建警报条件
│   │   alertcondition(bullishCross, "MACD看涨交叉")
│   │   alertcondition(bearishCross, "MACD看跌交叉")
│   │   ```
│   │
│   ├─ 价格水平突破
│   │   ```pine
│   │   // 支撑阻力突破
│   │   resistance = ta.highest(high, 20)
│   │   support = ta.lowest(low, 20)
│   │
│   │   alertcondition(ta.crossover(close, resistance),
│   │                  "突破阻力位")
│   │   alertcondition(ta.crossunder(close, support),
│   │                  "跌破支撑位")
│   │   ```
│   │
│   └─ 指标阈值触发
│       ```pine
│       // RSI超买超卖
│       rsi = ta.rsi(close, 14)
│       alertcondition(rsi > 70, "RSI超买")
│       alertcondition(rsi < 30, "RSI超卖")
│       ```
│
├─ 🔧 基本语法
│   │
│   ├─ 简单形式
│   │   ```pine
│   │   alertcondition(condition, title)
│   │   ```
│   │
│   ├─ 带消息
│   │   ```pine
│   │   alertcondition(condition, title, message)
│   │   ```
│   │
│   └─ 完整参数
│       ```pine
│       alertcondition(
│           condition,      // 条件表达式
│           title,          // 在警报对话框中显示的标题
│           message         // 警报消息模板
│       )
│       ```
│
├─ 📝 消息模板
│   │
│   ├─ 使用预定义变量
│   │   ```pine
│   │   alertcondition(
│   │       buySignal,
│   │       "买入信号",
│   │       "买入 {{ticker}} 在 {{close}} 价格"
│   │   )
│   │
│   │   // 可用变量：
│   │   // {{exchange}}, {{ticker}}, {{interval}}
│   │   // {{close}}, {{high}}, {{low}}, {{open}}
│   │   // {{time}}, {{timenow}}
│   │   ```
│   │
│   ├─ 自定义变量
│   │   ```pine
│   │   // ❌ 错误：不能使用自定义变量
│   │   alertcondition(signal, "信号", "价格: {{myPrice}}")
│   │
│   │   // ✅ 正确：使用内置变量
│   │   alertcondition(signal, "信号", "价格: {{close}}")
│   │   ```
│   │
│   └─ 多语言支持
│       ```pine
│       // 中文消息
│       alertcondition(buySignal, "买入",
│                      "在 {{close}} 买入 {{ticker}}")
│       ```
│
├─ ⚠️ 限制和注意事项
│   │
│   ├─ 仅限指标使用
│   │   ❌ 策略中不能使用 alertcondition()
│   │
│   ├─ 消息是静态的
│   │   ❌ 不能包含动态计算的值
│   │   ✅ 只能使用预定义变量
│   │
│   ├─ 计数限制
│   │   - 最多 20 个 alertcondition()
│   │   - 计入脚本的绘图计数
│   │
│   └─ 触发频率
│       - 仅在实时K线触发
│       - 需要用户在UI中激活
│
└─ 💡 最佳实践
    ├─ 清晰的标题
    │   ```pine
    │   // ✅ 好的标题
    │   alertcondition(signal, "MACD金叉（12,26,9）")
    │
    │   // ❌ 模糊的标题
    │   alertcondition(signal, "信号")
    │   ```
    │
    ├─ 描述性消息
    │   ```pine
    │   alertcondition(
    │       crossUp,
    │       "MA20上穿MA50",
    │       "移动平均线看涨交叉：{{ticker}} {{interval}}"
    │   )
    │   ```
    │
    └─ 组合条件
        ```pine
        // 多重确认
        strongBuy = rsi < 30 and close > ta.sma(close, 50)
        alertcondition(strongBuy, "强买入信号",
                      "RSI超卖且价格在MA之上")
        ```
```

## 🚨 alert() - 动态消息警报

```
┌─ 选择：alert()
│
├─ ✅ 适用场景
│   │
│   ├─ 动态价格警报
│   │   ```pine
│   │   // 自定义价格计算
│   │   entryPrice = ta.lowest(low, 5) * 1.02
│   │   if close > entryPrice and barstate.isconfirmed
│   │       alert(
│   │           "突破入场价: " + str.tostring(close) +
│   │           " 目标价: " + str.tostring(close * 1.05),
│   │           alert.freq_once_per_bar_close
│   │       )
│   │   ```
│   │
│   ├─ 多指标组合信号
│   │   ```pine
│   │   // 复合条件警报
│   │   rsi = ta.rsi(close, 14)
│   │   macd = ta.macd(close)[0]
│   │   volumeSpike = volume > ta.sma(volume, 20) * 2
│   │
│   │   if rsi < 30 and macd > 0 and volumeSpike
│   │       alertMsg = "多重确认买入信号:\n" +
│   │                    "RSI: " + str.tostring(rsi, "#.##") + "\n" +
│   │                    "MACD: " + str.tostring(macd, "#.####") + "\n" +
│   │                    "成交量: " + str.tostring(volume)
│   │       alert(alertMsg, alert.freq_once_per_bar)
│   │   ```
│   │
│   ├─ 实时监控警报
│   │   ```pine
│   │   // 实时价格变化警报
│   │   priceChange = math.abs(close - close[1]) / close[1] * 100
│   │   if priceChange > 5
│   │       alert("价格剧烈变化: " +
│   │              str.tostring(priceChange, "#.##") + "%",
│   │              alert.freq_all)
│   │   ```
│   │
│   └─ 策略状态警报
│       ```pine
│       // 策略状态变化
│       var bool inPosition = false
│       if strategy.position_size != 0 and not inPosition
│           inPosition := true
│           alert("进入仓位: " + str.tostring(strategy.position_avg_price))
│       else if strategy.position_size == 0 and inPosition
│           inPosition := false
│           alert("退出所有仓位")
│       ```
│
├─ 🔧 频率控制
│   │
│   ├─ alert.freq_once_per_bar
│   │   ```pine
│   │   // 每根K线仅触发一次
│   │   if condition
│   │       alert("信号", alert.freq_once_per_bar)
│   │   ```
│   │
│   ├─ alert.freq_once_per_bar_close
│   │   ```pine
│   │   // 仅在K线收盘时触发（避免重绘）
│   │   if condition and barstate.isconfirmed
│   │       alert("确认信号", alert.freq_once_per_bar_close)
│   │   ```
│   │
│   └─ alert.freq_all
│       ```pine
│       // 每次条件满足都触发（谨慎使用）
│       if realtimeCondition
│           alert("实时更新", alert.freq_all)
│       ```
│
├─ 📊 高级功能
│   │
│   ├─ 条件组合
│   │   ```pine
│   │   // 多条件警报
│   │   if condition1 and condition2 and barstate.isconfirmed
│   │       alert("组合条件满足", alert.freq_once_per_bar_close)
│   │   ```
│   │
│   ├─ 计数和限制
│   │   ```pine
│   │   // 限制警报频率
│   │   var int lastAlertBar = 0
│   │   minBarsBetween = 20
│   │
│   │   if condition and bar_index - lastAlertBar > minBarsBetween
│   │       alert("信号", alert.freq_once_per_bar)
│   │       lastAlertBar := bar_index
│   │   ```
│   │
│   └─ 格式化消息
│       ```pine
│       // 富文本格式
│       alertMsg = "🔥 " + title + "\n" +
│                  "价格: " + str.tostring(close, "#.##") + "\n" +
│                  "时间: " + str.format("{0,date,yyyy-MM-dd HH:mm}", time)
│       alert(alertMsg)
│       ```
│
├─ ⚠️ 注意事项
│   │
│   ├─ 实时限制
│   │   - alert() 仅在实时K线工作
│   │   - 历史K线不会触发警报
│   │
│   ├─ 性能考虑
│   │   - 避免过多警报调用
│   │   - 合理设置频率
│   │
│   └─ 消息长度
│       - 警报消息有长度限制
│       - 保持消息简洁
│
└─ 💡 最佳实践
    ├─ 使用 barstate.isconfirmed
    │   ```pine
    │   // 避免重绘导致的误报
    │   if signal and barstate.isconfirmed
    │       alert("确认信号", alert.freq_once_per_bar_close)
    │   ```
    │
    ├─ 清晰的消息格式
    │   ```pine
    │   // 结构化消息
    │   alert("【买入信号】\n" +
    │        "标的: {{ticker}}\n" +
    │        "价格: " + str.tostring(close) + "\n" +
    │        "指标: " + str.tostring(rsi, "#.##"))
    │   ```
    │
    └─ 错误处理
        ```pine
        // 验证数据后再发送警报
        if not na(close) and not na(volume) and condition
            alert("有效信号", alert.freq_once_per_bar)
        ```
```

## 📈 策略订单填充警报

```
┌─ 选择：策略订单警报
│
├─ ✅ 自动订单警报
│   │
│   └─ 订单执行时自动触发
│       ```pine
│       //@version=6
│       strategy("交易策略", overlay=true)
│
│       // 订单填充时自动触发警报
│       if ta.crossover(close, ta.sma(close, 20))
│           strategy.entry("Long", strategy.long,
│                         alert_message="买入订单执行")
│
│       if ta.crossunder(close, ta.sma(close, 20))
│           strategy.entry("Short", strategy.short,
│                         alert_message="卖出订单执行")
│       ```
│
├─ 🔧 自定义订单消息
│   │
│   ├─ 入场订单
│   │   ```pine
│       strategy.entry(
│           "Long",
│           strategy.long,
│           qty=0.1,
│           limit=entryPrice,
│           stop=stopLoss,
│           alert_message=
│               "买入执行 - 价格: {{strategy.order.price}} " +
│               "数量: {{strategy.order.size}} " +
│               "类型: {{strategy.order.comment}}"
│       )
│       ```
│   │
│   ├─ 出场订单
│   │   ```pine
│       strategy.exit(
│           "Exit Long",
│           "Long",
│           profit=100,
│           loss=50,
│           alert_message=
│               "退出多头 - 盈亏: {{strategy.order.comment}}"
│       )
│       ```
│   │
│   └─ 自定义字段
│       ```pine
│       // 使用 comment 传递额外信息
│       strategy.entry(
│           "Trade",
│           strategy.long,
│           comment="RSI:" + str.tostring(rsi, "#"),
│           alert_message="{{strategy.order.comment}}"
│       )
│       ```
│
├─ 📊 可用模板变量
│   │
│   ├─ 订单信息
│   │   - `{{strategy.order.price}}` - 执行价格
│   │   - `{{strategy.order.size}}` - 订单数量
│   │   - `{{strategy.order.comment}}` - 订单注释
│   │   - `{{strategy.order.id}}` - 订单ID
│   │
│   ├─ 策略信息
│   │   - `{{strategy.position_size}}` - 当前仓位
│   │   - `{{strategy.position_avg_price}}` - 平均价格
│   │   - `{{strategy.closed_trades}}` - 已平仓交易数
│   │
│   ├─ 性能指标
│   │   - `{{strategy.gross_profit}}` - 总利润
│   │   - `{{strategy.gross_loss}}` - 总亏损
│   │   - `{{strategy.netprofit}}` - 净利润
│   │
│   └─ 市场信息
│       - `{{ticker}}` - 交易品种
│       - `{{close}}` - 收盘价
│       - `{{time}}` - 时间
│
└─ 💡 高级用法
    ├─ 条件警报消息
    │   ```pine
    │   // 根据情况不同消息
    │   alertMsg = profit > 0 ?
    │                "盈利 {{strategy.order.comment}}" :
    │                "亏损 {{strategy.order.comment}}"
    │   strategy.exit(..., alert_message=alertMsg)
    │   ```
    │
    ├─ 动态计算
    │   ```pine
    │   // 包含计算值
    │   riskReward = reward / risk
    │   strategy.entry(...,
    │       alert_message=
    │           "风险收益比: " + str.tostring(riskReward, "#.##")
    │   )
    │   ```
    │
    └─ 多语言支持
        ```pine
        // 根据用户偏好
        alertMessage = language == "zh" ?
                       "买入执行" :
                       "Buy executed"
        strategy.entry(..., alert_message=alertMessage)
        ```
```

## 🔄 混合警报方案

```
┌─ 选择：多种警报组合
│
├─ 📊 指标 + 策略组合
│   └─ ```pine
│       //@version=6
│       indicator("混合警报示例", overlay=true)
│
│       // 1. alertcondition - 简单信号
│       buySignal = ta.crossover(ta.sma(close, 10), ta.sma(close, 20))
│       alertcondition(buySignal, "MA交叉信号")
│
│       // 2. alert() - 详细信息
│       if buySignal and barstate.isconfirmed
│           alert(
│               "MA金叉确认 - 价格: " + str.tostring(close) +
│               " 成交量: " + str.tostring(volume),
│               alert.freq_once_per_bar_close
│           )
│       ```
│
├─ 🎯 分级警报系统
│   └─ ```pine
│       // 三级警报系统
│       level1Signal = rsi > 70  // 初级警告
│       level2Signal = rsi > 80 and volumeSpike  // 中级警告
│       level3Signal = rsi > 90 and divergence  // 高级警告
│
│       // 不同级别不同处理
│       if level1Signal
│           alertcondition(true, "RSI超买警告")
│
│       if level2Signal
│           alert("强烈超买信号", alert.freq_once_per_bar)
│
│       if level3Signal
│           alert("极端超买！考虑反向", alert.freq_all)
│       ```
│
└─ 📈 多时间框架警报
    └─ ```pine
        // 多时间框架确认
        m5Signal = request.security(syminfo.tickerid, "5", ta.rsi(close, 14))
        h1Signal = request.security(syminfo.tickerid, "60", ta.rsi(close, 14))

        // 短期信号
        if ta.crossover(m5Signal, 30)
            alertcondition(true, "M5 RSI突破30")

        // 多时间框架确认
        if m5Signal > 30 and h1Signal > 30
            alert("多周期看涨确认", alert.freq_once_per_bar_close)
        ```
```

## 📋 警报测试清单

### 功能测试
- [ ] 警报是否在预期条件下触发？
- [ ] 消息内容是否正确？
- [ ] 频率设置是否合适？
- [ ] 是否避免误报？

### 性能测试
- [ ] 警报响应是否及时？
- [ ] 是否过多警报影响性能？
- [ ] 历史测试中表现如何？

### 实用性测试
- [ ] 警报信息是否足够？
- [ ] 是否可操作？
- [ ] 用户是否容易理解？

## ⚠️ 常见问题

1. **警报不触发**
   - 检查是否在实时K线
   - 确认警报已激活
   - 验证条件逻辑

2. **重复警报**
   - 调整频率设置
   - 添加冷却期
   - 使用 barstate.isconfirmed

3. **消息格式问题**
   - 检查变量名
   - 验证字符串拼接
   - 控制消息长度

4. **性能问题**
   - 减少警报检查频率
   - 优化条件逻辑
   - 避免复杂计算

## 💡 总结

| 警报类型 | 适用场景 | 优点 | 缺点 |
|---------|---------|------|------|
| alertcondition() | 简单条件，用户UI选择 | 简单，用户可控 | 消息静态，功能有限 |
| alert() | 动态消息，复杂条件 | 灵活，消息动态 | 需要编程实现 |
| 订单警报 | 策略交易 | 自动触发，详细信息 | 仅限策略使用 |

选择警报方式的关键：**匹配需求复杂度，考虑用户体验，保证可靠性**。