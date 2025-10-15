# 脚本类型选择决策树

## 🎯 起始问题：我需要创建什么类型的脚本？

```
┌─────────────────────────────────────────────────────┐
│         🤔 你想创建什么？                          │
└─────────────────────────────────────────────────────┘
    │
    ├─ 📊 分析和显示数据
    │   │
    │   ├─ 只显示图形和指标？
    │   │   └─ ✅ **使用 Indicator**
    │   │       ```pine
    │   │       indicator("我的指标", overlay=true)
    │   │       ```
    │   │
    │   └─ 需要其他脚本复用功能？
    │       └─ ✅ **使用 Library**
    │           ```pine
    │           library("我的库", 2, overlay=false)
    │           export myFunction() =>
    │               // 实现代码
    │           ```
    │
    └─ 💰 模拟交易和回测
        │
        └─ ✅ **使用 Strategy**
            ```pine
            strategy("我的策略", overlay=true)
            ```
```

## 详细决策流程

### 📊 Indicator 路径

```
┌─ 你选择了 Indicator
│
├─ 🎨 显示在主图还是副图？
│   ├─ 主图（价格图上）
│   │   └─ indicator("名称", overlay=true)
│   └─ 副图（独立窗口）
│       └─ indicator("名称", overlay=false)
│
├─ 📈 需要多个输出吗？
│   ├─ 是 → 考虑 plot 数量限制（最多 55个）
│   └─ 否 → 单个 plot 即可
│
├─ 🔔 需要警报功能？
│   ├─ 简单警报 → 使用 alertcondition()
│   │   ```pine
│   │   alertcondition(buySignal, "买入信号")
│   │   ```
│   └─ 复杂警报 → 使用 alert()
│       ```pine
│       if buySignal
│           alert("买入信号触发！", alert.freq_once_per_bar)
│       ```
│
└─ 💡 特殊需求？
    ├─ 需要输入参数 → 使用 input.*()
    ├─ 需要颜色自定义 → 使用 input.color()
    └─ 需要样式选项 → 使用 input.style()
```

### 💰 Strategy 路径

```
┌─ 你选择了 Strategy
│
├─ 💵 交易方向？
│   ├─ 仅做多
│   │   └─ strategy("名称", default_qty_type=strategy.percent_of_equity, default_qty_value=100)
│   ├─ 仅做空
│   │   └─ strategy("名称", shorttitle="做空", default_qty_type=strategy.percent_of_equity)
│   └─ 双向交易
│       └─ strategy("名称", default_qty_type=strategy.percent_of_equity)
│
├─ ⏰ 订单执行时机？
│   ├─ 仅收盘价
│   │   └─ calc_on_every_tick=false
│   └─ 每个tick
│       └─ calc_on_every_tick=true
│       ⚠️ 可能导致重绘
│
├─ 💰 资金管理？
│   ├─ 固定数量
│   │   └─ default_qty_type=strategy.fixed
│   ├─ 百分比权益
│   │   └─ default_qty_type=strategy.percent_of_equity
│   └─ 固定金额
│       └─ default_qty_type=strategy.cash
│
├─ 📊 手续费和滑点？
│   ├─ 使用默认
│   │   └─ commission_type=strategy.commission.percent
│   └─ 自定义
│       └─ 设置 commission_value, slippage
│
└─ 🎯 退出策略？
    ├─ 固定止盈止损
    │   └─ strategy.exit("退出", "入场", profit=100, loss=50)
    ├─ 动态退出
    │   └─ strategy.close("入场", when=exitCondition)
    └─ 时间退出
        └─ strategy.close_all(when=time >= timestamp(syminfo.tickerid, "2300-01-01"))
```

### 📚 Library 路径

```
┌─ 你选择了 Library
│
├─ 📦 需要导出什么？
│   ├─ 函数
│   │   ```pine
│   │   export calculateRSI(source, length) =>
│   │       ta.rsi(source, length)
│   │   ```
│   ├─ 类型
│   │   ```pine
│   │   export type MyType
│   │       float value
│   │       string name
│   │   ```
│   └─ 枚举
│       ```pine
│       export enum Mode
│           FAST = 1
│           SLOW = 2
│       ```
│
├─ 🔄 版本控制？
│   └─ library("名称", 版本号)
│       ```pine
│       library("我的工具库", 2)
│       ```
│
├─ 📥 导入使用？
│   ```pine
│   import myLib as lib from "MyLibrary/1"
│   result = lib.calculateRSI(close, 14)
│   ```
│
└─ 💡 最佳实践
    ├─ 相关功能组织在一起
    ├─ 清晰的函数文档
    ├─ 合理的版本管理
    └─ 避免循环依赖
```

## 决策检查清单

### Indicator 适用场景
- [ ] 需要显示技术指标
- [ ] 需要分析价格行为
- [ ] 需要视觉化数据
- [ ] 不涉及实际交易

### Strategy 适用场景
- [ ] 需要模拟交易
- [ ] 需要回测功能
- [ ] 需要性能指标
- [ ] 需要订单管理

### Library 适用场景
- [ ] 代码需要复用
- [ ] 创建通用工具
- [ ] 组织复杂项目
- [ ] 提供API接口

## 转换可能性

```
┌──────────────────────┐    ┌──────────────────────┐
│    Indicator         │    │      Strategy         │
│ (可以转换为 Strategy) │◄──►│ (可以简化为 Indicator)│
└──────────────────────┘    └──────────────────────┘
                                      │
                                      ▼
                               ┌──────────────────────┐
                               │      Library          │
                               │ (可提取公共部分)     │
                               └──────────────────────┘
```

## 常见错误避免

1. ❌ 在 Indicator 中使用 strategy 函数
2. ❌ 在 Strategy 中缺少风险控制
3. ❌ Library 中直接访问图表数据
4. ❌ 混淆 overlay 参数设置

## 示例代码模板

### Indicator 模板
```pine
//@version=6
indicator("我的指标", shorttitle="MI", overlay=true, timeframe="", timeframe_gaps=false)

// 输入参数
len = input.int(14, "周期")
src = input.source(close, "源")

// 计算
ma = ta.sma(src, len)

// 绘图
plot(ma, color=color.blue, title="MA")
```

### Strategy 模板
```pine
//@version=6
strategy("我的策略", overlay=true,
         default_qty_type=strategy.percent_of_equity,
         default_qty_value=100,
         commission_type=strategy.commission.percent,
         commission_value=0.1)

// 输入参数
len = input.int(14, "MA周期")
risk = input.float(2.0, "风险%") / 100

// 计算
ma = ta.sma(close, len)
longCond = ta.crossover(close, ma)
shortCond = ta.crossunder(close, ma)

// 交易逻辑
if longCond
    strategy.entry("Long", strategy.long)
if shortCond
    strategy.entry("Short", strategy.short)

// 风险管理
stopLoss = strategy.position_avg_price * (1 - risk)
takeProfit = strategy.position_avg_price * (1 + risk * 2)
strategy.exit("Exit", "Long", stop=stopLoss, limit=takeProfit)
```

### Library 模板
```pine
//@version=6
library("技术指标库", 2)

// 导出函数
export type MACD
    float macd
    float signal
    float histogram

export calculateMACD(source, fastLength, slowLength, signalLength) =>
    fastMA = ta.ema(source, fastLength)
    slowMA = ta.ema(source, slowLength)
    macdLine = fastMA - slowMA
    signalLine = ta.sma(macdLine, signalLength)
    histogram = macdLine - signalLine
    [macdLine, signalLine, histogram]
```