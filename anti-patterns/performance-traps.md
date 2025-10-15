# 性能陷阱反例

性能问题会导致脚本运行缓慢、达到计算限制，甚至无法正常工作。以下是常见的性能陷阱。

## 1. 循环中的重复计算

### ❌ 错误示例：循环内重复计算
```pine
//@version=6
indicator("错误：循环内重复计算")

// ❌ 每次循环都重新计算相同的值
var float[] results = array.new<float>()
for i = 0 to 50
    // 每次都重新计算MA，非常低效
    ma20 = ta.sma(close, 20)
    value = close - ma20
    array.push(results, value)
```

### 🚨 问题说明
- `ta.sma(close, 20)` 在循环中计算了51次相同的值
- 随着循环次数增加，计算时间呈指数增长
- 可能触发 Pine Script 的计算时间限制

### ✅ 正确做法：预计算值
```pine
//@version=6
indicator("正确：预计算值")

// ✅ 在循环外计算一次
ma20 = ta.sma(close, 20)
var float[] results = array.new<float>()

for i = 0 to 50
    // 使用预计算的值
    value = close - ma20
    array.push(results, value)
```

## 2. 无限制增长的数组

### ❌ 错误示例：数组无限增长
```pine
//@version=6
indicator("错误：内存泄漏")

// ❌ 数组不断增长，永不清理
var float[] priceHistory = array.new<float>()

// 每根K线都添加数据，从不删除
if barstate.isconfirmed
    array.push(priceHistory, close)

// 可能导致内存耗尽
avgPrice = array.avg(priceHistory)
plot(avgPrice, "平均价格")
```

### 🚨 问题说明
- 数组大小无限增长，最终达到 Pine Script 限制
- 每次计算平均都需要遍历整个数组
- 随着时间推移，性能急剧下降

### ✅ 正确做法：限制数组大小
```pine
//@version=6
indicator("正确：固定大小数组")

// ✅ 限制数组最大大小
var float[] priceHistory = array.new<float>()
maxSize = 200

if barstate.isconfirmed
    array.unshift(priceHistory, close)
    // 保持数组大小不变
    if array.size(priceHistory) > maxSize
        array.pop(priceHistory)

// 计算高效的平均值
avgPrice = array.avg(priceHistory)
plot(avgPrice, "平均价格")
```

## 3. 过度使用 request.security()

### ❌ 错误示例：频繁调用跨周期请求
```pine
//@version=6
indicator("错误：频繁跨周期请求")

// ❌ 每个tick都请求多个时间框架
m5_rsi = request.security(syminfo.tickerid, "5", ta.rsi(close, 14))
m15_rsi = request.security(syminfo.tickerid, "15", ta.rsi(close, 14))
h1_rsi = request.security(syminfo.tickerid, "60", ta.rsi(close, 14))
h4_rsi = request.security(syminfo.tickerid, "240", ta.rsi(close, 14))

// 在策略中频繁调用
if m5_rsi > 50 and m15_rsi > 50 and h1_rsi > 50 and h4_rsi > 50
    // 交易逻辑
```

### 🚨 问题说明
- `request.security()` 是昂贵的操作
- 在每个tick上调用会严重影响性能
- 多个调用会触发服务器限制

### ✅ 正确做法：缓存和条件请求
```pine
//@version=6
indicator("正确：缓存跨周期数据")

// ✅ 使用var缓存数据
var float m5_rsi = na
var float m15_rsi = na
var float h1_rsi = na
var float h4_rsi = na

// 只在需要时更新
updateMTF = barstate.isconfirmed

if updateMTF
    // 批量请求
    m5_rsi := request.security(syminfo.tickerid, "5", ta.rsi(close, 14)[1])
    m15_rsi := request.security(syminfo.tickerid, "15", ta.rsi(close, 14)[1])
    h1_rsi := request.security(syminfo.tickerid, "60", ta.rsi(close, 14)[1])
    h4_rsi := request.security(syminfo.tickerid, "240", ta.rsi(close, 14)[1])

// 使用缓存的数据
if m5_rsi > 50 and m15_rsi > 50 and h1_rsi > 50 and h4_rsi > 50
    // 交易逻辑
```

## 4. 过深的嵌套循环

### ❌ 错误示例：嵌套循环
```pine
//@version=6
indicator("错误：嵌套循环")

// ❌ 嵌套循环，性能灾难
var float[][] matrix = matrix.new<float>(50, 50)

for i = 0 to 49
    for j = 0 to 49
        // 2500次循环！
        matrix.set(matrix, i, j, close * (i + j))
```

### 🚨 问题说明
- 嵌套循环的复杂度是 O(n²)
- 50×50 = 2500次操作
- Pine Script 循环限制是100次，这会导致错误

### ✅ 正确做法：向量化操作
```pine
//@version=6
indicator("正确：向量化操作")

// ✅ 避免嵌套循环
var float[] vector = array.new<float>()

// 使用内置函数
for i = 0 to 49
    value = close * i
    array.push(vector, value)

// 如果真的需要矩阵，分步操作
// 或者考虑是否真的需要这么多计算
```

## 5. 不必要的绘图对象

### ❌ 错误示例：创建过多绘图对象
```pine
//@version=6
indicator("错误：过多绘图对象")

// ❌ 为每个数据点创建标签
var label[] labels = array.new<label>()

// 无限制创建标签
for i = 0 to 100
    if close > ta.sma(close, 20)
        newLabel = label.new(bar_index - i, high[i], "高价",
                           color.red, size.small)
        array.push(labels, newLabel)
```

### 🚨 问题说明
- 标签数量无限增长
- 每个标签都消耗内存
- 图表变得非常缓慢

### ✅ 正确做法：限制和清理
```pine
//@version=6
indicator("正确：限制绘图对象")

// ✅ 限制最大标签数量
var label[] labels = array.new<label>()
maxLabels = 10

// 只在需要时创建
if close > ta.sma(close, 20)
    newLabel = label.new(bar_index, high, "高价",
                       color.red, size.small)
    array.unshift(labels, newLabel)

    // 清理旧标签
    if array.size(labels) > maxLabels
        oldLabel = array.pop(labels)
        label.delete(oldLabel)
```

## 6. 重复的复杂计算

### ❌ 错误示例：重复计算复杂指标
```pine
//@version=6
indicator("错误：重复计算")

// ❌ 多次计算相同的复杂指标
if ta.rsi(close, 14) > 70
    // 过度条件
    if ta.rsi(close, 14) > 80
        // 超级条件
        plotshape(1, "超买", style=shape.triangledown)

    // 计算MACD（也是重复的）
    [macdLine, signalLine] = ta.macd(close, 12, 26, 9)
    if macdLine > signalLine
        plotshape(1, "背离", style=shape.circle)
```

### 🚨 问题说明
- `ta.rsi(close, 14)` 计算了多次
- `ta.macd()` 在多个地方调用
- 复杂指标的计算成本很高

### ✅ 正确做法：缓存计算结果
```pine
//@version=6
indicator("正确：缓存计算")

// ✅ 一次计算，多次使用
rsi14 = ta.rsi(close, 14)
[macdLine, signalLine] = ta.macd(close, 12, 26, 9)

// 使用缓存的值
if rsi14 > 70
    if rsi14 > 80
        plotshape(1, "超买", style=shape.triangledown)

    if macdLine > signalLine
        plotshape(1, "背离", style=shape.circle)
```

## 7. 不必要的字符串操作

### ❌ 错误示例：频繁字符串拼接
```pine
//@version=6
indicator("错误：频繁字符串操作")

// ❌ 每次都拼接字符串
for i = 0 to 20
    message = "价格: " + str.tostring(close[i]) +
              " 时间: " + str.format("{0,date,yyyy-MM-dd}", time[i]) +
              " RSI: " + str.tostring(ta.rsi(close[i], 14))
    // 使用message
```

### 🚨 问题说明
- 字符串操作在 Pine Script 中很昂贵
- 在循环中进行字符串拼接会严重影响性能
- 每次拼接都创建新的字符串对象

### ✅ 正确做法：减少字符串操作
```pine
//@version=6
indicator("正确：减少字符串操作")

// ✅ 只在需要时创建字符串
// 预计算数值
rsi14 = ta.rsi(close, 14)

// 只在最后一根K线显示详细信息
if barstate.islast
    message = "价格: " + str.tostring(close) +
              " RSI: " + str.tostring(rsi14)
    label.new(bar_index, high, message)
```

## 8. 忽略早期退出

### ❌ 错误示例：不必要的完整循环
```pine
//@version=6
indicator("错误：不必要的完整循环")

// ❌ 即使找到目标也继续循环
var float[] data = array.from(1, 5, 10, 15, 20, 25, 30)
target = 15
foundIndex = -1

for i = 0 to array.size(data) - 1
    if array.get(data, i) == target
        foundIndex := i
    // 继续循环，浪费时间
```

### 🚨 问题说明
- 找到目标后继续循环
- 没有使用 break 语句（Pine Script 不支持，但可以模拟）
- 浪费不必要的计算资源

### ✅ 正确做法：条件退出
```pine
//@version=6
indicator("正确：条件退出")

// ✅ 找到目标后退出
var float[] data = array.from(1, 5, 10, 15, 20, 25, 30)
target = 15
foundIndex = -1

for i = 0 to array.size(data) - 1
    if array.get(data, i) == target
        foundIndex := i
        break  // 使用 break 提前退出
    // 找到后不会执行
```

## 9. 过度使用历史引用

### ❌ 错误示例：深度历史引用
```pine
//@version=6
indicator("错误：深度历史引用")

// ❌ 引用过多的历史数据
volatility = ta.stdev(ta.change(close, 1), 100) * 100
veryOldMA = ta.sma(close, 500)  // 引用500根K线前
ancientHigh = ta.highest(high, 1000)  // 引用1000根K线前

// 每个引用都需要访问历史数据
plot(volatility, "波动率")
plot(veryOldMA, "500MA")
```

### 🚨 问题说明
- 深度历史引用需要加载大量历史数据
- 每次计算都需要遍历历史数据
- 在低时间框架上尤其缓慢

### ✅ 正确做法：合理的历史长度
```pine
//@version=6
indicator("正确：合理历史长度")

// ✅ 使用合理的历史长度
volatility = ta.stdev(ta.change(close, 1), 20) * 100  // 20周期足够
recentMA = ta.sma(close, 100)  // 100周期更实用
recentHigh = ta.highest(high, 50)  // 50周期高点的近期参考

plot(volatility, "波动率")
plot(recentMA, "100MA")
```

## 10. 忽略条件计算

### ❌ 错误示例：总是计算所有内容
```pine
//@version=6
indicator("错误：总是计算")

// ❌ 即使不需要也计算所有指标
rsi = ta.rsi(close, 14)
macd = ta.macd(close, 12, 26, 9)
bb = ta.bb(close, 20, 2)
stoch = ta.stoch(close, high, low, 14)

// 即使只显示一个也计算所有
showRSI = input.bool(false)
if showRSI
    plot(rsi, "RSI")
```

### 🚨 问题说明
- 计算了不需要的指标
- 浪费 CPU 资源
- 增加脚本加载时间

### ✅ 正确做法：条件计算
```pine
//@version=6
indicator("正确：条件计算")

// ✅ 只计算需要的内容
showRSI = input.bool(false)
showMACD = input.bool(false)
showBB = input.bool(false)

// 条件计算
var float rsi = na
var float macd = na
var [bbUpper, bbMiddle, bbLower] = [na, na, na]

if showRSI
    rsi := ta.rsi(close, 14)
    plot(rsi, "RSI")

if showMACD
    [macd, signal, hist] = ta.macd(close, 12, 26, 9)
    plot(macd, "MACD")

if showBB
    [bbUpper, bbMiddle, bbLower] = ta.bb(close, 20, 2)
    plot(bbUpper, "BB上轨")
    plot(bbMiddle, "BB中轨")
    plot(bbLower, "BB下轨")
```

## 性能优化检查清单

1. **是否有循环内的重复计算？**
2. **数组是否有无限增长的风险？**
3. **request.security() 调用是否过于频繁？**
4. **是否有不必要的嵌套循环？**
5. **绘图对象数量是否得到控制？**
6. **复杂指标是否被缓存？**
7. **字符串操作是否最小化？**
8. **是否合理使用历史引用？**
9. **是否有条件计算的需要？**
10. **是否找到后能提前退出循环？**

## 性能优化黄金法则

1. **预计算**：循环外计算，循环内使用
2. **限制大小**：数组和对象要有上限
3. **缓存数据**：昂贵的操作要缓存结果
4. **条件执行**：不需要就不计算
5. **批量操作**：使用内置函数代替循环
6. **及时清理**：定期清理不需要的对象
7. **合理引用**：不要过度依赖历史数据

记住：**性能优化是平衡的艺术，先让它正确，再让它快速。**