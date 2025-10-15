# 性能优化决策树

## ⚡ 起始问题：脚本运行缓慢或达到计算限制？

```
┌─────────────────────────────────────────────────────┐
│   ⚠️ Pine Script 性能限制：                         │
│   • 循环最多100次迭代                               │
│   • 请求.security() 限制调用频率                   │
│   • 每个脚本有计算时间限制                          │
│   • 绘图对象数量限制（标签、线条等）               │
└─────────────────────────────────────────────────────┘
    │
    └─ 🔍 症状识别？
        │
        ├─ 循环报错/限制错误
        │   └─ ➡️ **跳转到循环优化**
        │
        ├─ 脚本加载慢
        │   └─ ➡️ **跳转到计算优化**
        │
        ├─ 图表显示慢
        │   └─ ➡️ **跳转到绘图优化**
        │
        └─ 多时间框架数据慢
            └─ ➡️ **跳转到跨周期优化**
```

## 🔄 循环优化路径

```
┌─ 问题：循环性能瓶颈
│
├─ 📊 循环类型？
│   │
│   ├─ for 循环
│   │   └─ 🔧 优化策略：
│   │       ```pine
│   │       // ❌ 错误：不必要的长循环
│   │       for i = 0 to 99
│   │           array.push(arr, ta.sma(close, i + 1))
│   │
│   │       // ✅ 正确：使用内置函数
│   │       values = array.new<float>()
│   │       array.push(values, ta.sma(close, 100))
│   │       ```
│   │
│   ├─ while 循环
│   │   └─ 🔧 优化策略：
│   │       ```pine
│   │       // ❌ 危险：可能无限循环
│   │       while condition
│   │           // 处理
│   │
│   │       // ✅ 安全：添加计数器
│   │       counter = 0
│   │       while condition and counter < 100
│   │           counter += 1
│   │       ```
│   │
│   └─ array 循环操作
│       └─ 🔧 使用内置方法：
│           ```pine
           // ❌ 慢：手动遍历
           sum = 0.0
           for i = 0 to array.size(arr) - 1
               sum += array.get(arr, i)

           // ✅ 快：使用内置函数
           sum = array.sum(arr)
           avg = array.avg(arr)
│           ```
│
├─ 💡 循环优化技巧
│   │
│   ├─ 提前退出
│   │   ```pine
│   │   // 找到目标后立即退出
│   │   for i = 0 to array.size(arr) - 1
│   │       if array.get(arr, i) == target
│   │           break
│   │   ```
│   │
│   ├─ 减少循环内计算
│   │   ```pine
│   │   // ❌ 重复计算
│   │   for i = 0 to len
│   │       result = ta.sma(close, 20) * i
│   │
│   │   // ✅ 预计算
│   │   baseValue = ta.sma(close, 20)
│   │   for i = 0 to len
│   │       result = baseValue * i
│   │   ```
│   │
│   ├─ 批量操作
│   │   ```pine
│   │   // 使用 array.fill, array.slice 等批量方法
│   │   ```
│   │
│   └─ 缓存结果
│       ```pine
│       // 使用 var 缓存计算结果
│       var cachedValue = na
│       if na(cachedValue)
│           cachedValue := expensiveCalculation()
│       ```
│
└─ 📈 循环替代方案
    ├─ 使用内置函数替代
    ├─ 使用数学公式替代
    └─ 使用向量化操作
```

## ⚙️ 计算优化路径

```
┌─ 问题：脚本计算慢
│
├─ 🎯 计算频率优化
│   │
│   ├─ 每个K线都计算？
│   │   └─ 📝 检查 calc_on_every_tick
│   │       ```pine
│   │       // ❌ 实时每个tick都计算
│   │       strategy("策略", calc_on_every_tick=true)
│   │
│   │       // ✅ 仅在K线收盘时计算
│   │       strategy("策略", calc_on_every_tick=false)
│   │       ```
│   │
│   └─ 减少不必要的计算
│       ```pine
│       // ❌ 每次都计算
│       ma20 = ta.sma(close, 20)
│       ma50 = ta.sma(close, 50)
│       ma200 = ta.sma(close, 200)
│       even if not needed
│
│       // ✅ 条件计算
│       ma20 = input.bool(true, "显示MA20") ? ta.sma(close, 20) : na
│       ```
│
├─ 📊 数学运算优化
│   │
│   ├─ 避免复杂运算
│   │   ```pine
│   │   // ❌ 慢：多次幂运算
│   │   result = math.pow(x, 2) + math.pow(y, 2)
│   │
│   │   // ✅ 快：直接乘法
│   │   result = x * x + y * y
│   │   ```
│   │
│   ├─ 使用近似值
│   │   ```pine
│   │   // ❌ 精确但慢
│   │   sqrt = math.sqrt(value)
│   │
│   │   // ✅ 近似但快
│   │   sqrt = value * 0.5  // 某些场景下
│   │   ```
│   │
│   └─ 避免类型转换
│       ```pine
│       // ❌ 多次转换
│       result = int(string(floatValue))
│
│       // ✅ 保持类型一致
│       result = int(floatValue)
│       ```
│
├─ 🔄 函数调用优化
│   │
│   ├─ 缓存函数结果
│   │   ```pine
│   │   // ❌ 重复调用
│   │   plot(ta.rsi(close, 14))
│   │   plot(ta.rsi(close, 14) - 30)
│   │
│   │   // ✅ 缓存结果
│   │   rsi14 = ta.rsi(close, 14)
│   │   plot(rsi14)
│   │   plot(rsi14 - 30)
│   │   ```
│   │
│   ├─ 减少自定义函数调用
│   │   ```pine
│   │   // ❌ 每次调用都计算
│   │   calculateMA() =>
│   │       ta.sma(close, 20)
│   │
│   │   // ✅ 内联计算
│   │   ma20 = ta.sma(close, 20)
│   │   ```
│   │
│   └─ 使用高效算法
│       ```pine
       // 选择时间复杂度低的算法
│       ```
│
└─ 📝 条件优化
    ├─ 短路求值
    │   ```pine
    │   // ✅ 先判断轻量级条件
    │   if lightCondition and heavyCondition
    │       // 处理
    │   ```
    │
    ├─ 减少嵌套
    │   ```pine
    │   // ❌ 深层嵌套
    │   if a
    │       if b
    │           if c
    │               // 处理
    │
    │   // ✅ 扁平结构
    │   if a and b and c
    │       // 处理
    │   ```
    │
    └─ 使用 switch 代替多重 if
        ```pine
        // ✅ 更清晰高效
        switch mode
            "MA" => ta.sma(close, len)
            "EMA" => ta.ema(close, len)
            "WMA" => ta.wma(close, len)
        => ta.sma(close, len)
        ```
```

## 🎨 绘图优化路径

```
┌─ 问题：图表显示慢
│
├─ 📊 绘图对象数量
│   │
│   ├─ plot 对象过多？
│   │   └─ 📝 减少或合并
│   │       ```pine
│   │       // ❌ 多个独立plot
│   │       plot(ma20)
│   │       plot(ma50)
│   │       plot(ma200)
│   │
│   │       // ✅ 合并显示
│   │       plot(ma20, "MA20", color.blue)
│   │       plot(ma50, "MA50", color.red)
│   │       // 或使用 colors 参数
│   │       ```
│   │
│   ├─ 标签/线条过多？
│   │   └─ 📝 限制数量或清理
│   │       ```pine
│   │       // ❌ 无限制创建
│   │       if condition
│   │           label.new(bar_index, high, "标记")
│   │
│   │       // ✅ 限制数量
│   │       var label[] labels = array.new<label>()
│   │       if condition and array.size(labels) < 10
│   │           array.push(labels, label.new(...))
│   │
│   │       // ✅ 清理旧标签
│   │       if barstate.isconfirmed
│   │           label.delete(array.shift(labels))
│   │       ```
│   │
│   └─ 表格更新频繁？
│       └─ 📝 优化更新频率
│           ```pine
│           // ❌ 每个tick都更新
│           if barstate.isrealtime
│               table.cell(...)
│
│           // ✅ 仅在需要时更新
│           if condition and barstate.isconfirmed
│               table.cell(...)
│           ```
│
├─ 🎨 视觉效果优化
│   │
│   ├─ 复杂颜色计算
│   │   ```pine
│   │   // ❌ 每次都计算颜色
│   │   plotColor = rsi > 70 ? color.red :
│   │               rsi < 30 ? color.green :
│   │               color.blue
│   │
│   │   // ✅ 缓存颜色
│   │   var plotColor = color.blue
│   │   if rsi > 70
│   │       plotColor := color.red
│   │   else if rsi < 30
│   │       plotColor := color.green
│   │   ```
│   │
│   ├─ 透明度渐变
│   │   ```pine
│   │   // ❌ 复杂计算
│   │   alpha = math.abs(rsi - 50) * 2.55
│   │
│   │   // ✅ 使用阶梯值
│   │   alpha = rsi > 60 ? 80 : rsi < 40 ? 40 : 60
│   │   ```
│   │
│   └─ 样式切换
│       ```pine
       // 使用 style 参数优化显示
       plot(value, style=plot.style_area)
│       ```
│
└─ 📈 条件绘图
    ├─ 减少不必要的绘制
    │   ```pine
    │   // ❌ 总是绘制
    │   plot(signal, "信号")
    │
    │   // ✅ 条件绘制
    │   plot(showSignals ? signal : na, "信号")
    │   ```
    │
    └─ 使用 display 参数
        ```pine
        // 控制显示范围
        plot(ma, display=display.none)  // 仅在数据窗口显示
        ```
```

## 📊 跨周期优化路径

```
┌─ 问题：request.security() 性能问题
│
├─ 🔄 调用频率
│   │
│   ├─ 每个K线都请求？
│   │   └─ 📝 减少请求次数
│   │       ```pine
│   │       // ❌ 每次都请求
│   │       higherTF = request.security(..., close)
│   │
│   │       // ✅ 缓存结果
│   │       var higherTF = na
│   │       if barstate.isconfirmed
│   │           higherTF := request.security(..., close[1])
│   │       ```
│   │
│   └─ 请求多个值？
│       └─ 📝 批量请求
│           ```pine
│           // ❌ 多次请求
│           high_tf = request.security(..., high)
│           low_tf = request.security(..., low)
│           close_tf = request.security(..., close)
│
│           // ✅ 一次请求
│           [h, l, c] = request.security(...,
│               [high, low, close])
│           ```
│
├─ 📊 请求的数据量
│   │
│   ├─ 请求长周期数据？
│   │   └─ 📝 使用 lookahead=barmerge.lookahead_on
│   │       ```pine
│   │       // ✅ 明确设置lookahead
│   │       data = request.security(...,
│           close,
│           lookahead=barmerge.lookahead_on)
│   │       ```
│   │
│   └─ 请求多个时间框架？
│       └─ 📝 优先级排序
│           ```pine
│           // 按重要性排序请求
│           primary = request.security(..., primaryData)
│           if time > lastRequestTime
│               secondary = request.security(..., secondaryData)
│           ```
│
└─ 💡 缓存策略
    ├─ 使用 var 缓存
    │   ```pine
    │   // 缓存跨周期数据
    │   var cachedData = array.new<float>()
    │   ```
    │
    ├─ 定时更新
    │   ```pine
    │   // 每小时更新一次
    │   if ta.change(time('60'))
    │       cachedData := updateData()
    │   ```
    │
    └─ 按需更新
        ```pine
        // 仅在需要时更新
        if needUpdate and barstate.isconfirmed
            updateData()
        ```
```

## 🛠️ 通用优化策略

### 1. 代码结构优化
```pine
// ❌ 分散计算
a = calculateA()
b = calculateB()
c = calculateC()

// ✅ 组织计算
calculateAll() =>
    [calculateA(), calculateB(), calculateC()]
[a, b, c] = calculateAll()
```

### 2. 数据结构优化
```pine
// ❌ 多个变量
var float val1 = na
var float val2 = na
var float val3 = na

// ✅ 使用数组
var values = array.new<float>(3, 0.0)
```

### 3. 条件执行优化
```pine
// ❌ 总是执行
heavyCalculation()

// ✅ 条件执行
if needCalculation and barstate.isconfirmed
    heavyCalculation()
```

## 📊 性能检测工具

### 1. 内置检查
```pine
// 检查计算时间
start = timenow
result = heavyCalculation()
elapsed = timenow - start
if elapsed > 100  // 超过100ms
    label.new(bar_index, high, "慢计算: " + str.tostring(elapsed) + "ms")
```

### 2. 循环计数器
```pine
// 监控循环次数
var loopCount = 0
for i = 0 to array.size(arr) - 1
    loopCount += 1
    if loopCount > 90
        runtime.error("接近循环限制！")
```

### 3. 内存使用检查
```pine
// 检查数组大小
if array.size(hugeArray) > 10000
    runtime.error("数组过大！")
```

## 💡 性能优化清单

- [ ] 减少不必要的计算
- [ ] 缓存重复使用的值
- [ ] 优化循环（减少迭代次数）
- [ ] 使用内置函数代替自定义实现
- [ ] 限制绘图对象数量
- [ ] 优化 request.security() 调用
- [ ] 使用合适的数据结构
- [ ] 条件执行重计算
- [ ] 简化数学运算
- [ ] 避免频繁的类型转换
- [ ] 使用 var 持久化变量
- [ ] 批量操作代替单个操作

## ⚠️ 常见性能陷阱

1. **过度使用 request.security()**
2. **在循环中进行复杂计算**
3. **创建过多的绘图对象**
4. **每个tick都更新所有数据**
5. **不必要的历史引用**
6. **深层嵌套的条件判断**
7. **重复的字符串操作**
8. **不必要的数据类型转换**

记住：**优化是平衡的艺术**。在追求性能的同时，也要考虑代码的可读性和维护性。先让代码正确，再让它快速。