# Pine Script 常见错误总结

## 📊 错误统计

以下是 Pine Script 开发中最容易犯的错误，按发生频率排序：

| 错误类型 | 发生频率 | 影响等级 | 容易发现 |
|---------|---------|---------|---------|
| 重绘错误 | 极高 | 严重 | 困难 |
| 性能问题 | 高 | 中等 | 中等 |
| 逻辑错误 | 高 | 严重 | 困难 |
| 数据结构误用 | 中等 | 中等 | 容易 |
| 类型错误 | 低 | 严重 | 容易 |

## 🚫 十大致命错误

### 1. **未来泄漏** (最严重)
```pine
// ❌ 致命错误
dailyClose = request.security(syminfo.tickerid, "D", close)

// ✅ 正确做法
dailyClose = request.security(syminfo.tickerid, "D", close[1])
```

### 2. **实时数据误用**
```pine
// ❌ 会导致重绘
if ta.crossover(close, ta.sma(close, 20))
    strategy.entry("Long", strategy.long)

// ✅ 等待确认
if ta.crossover(close, ta.sma(close, 20)) and barstate.isconfirmed
    strategy.entry("Long", strategy.long)
```

### 3. **无限循环**
```pine
// ❌ 危险：可能无限循环
var float value = 0
value := ta.sma(value, 10)  // 循环引用

// ✅ 正确计算
rawValue = close * 0.1
value := ta.sma(rawValue, 10)
```

### 4. **数组越界**
```pine
// ❌ 运行时错误
value = array.get(arr, array.size(arr))

// ✅ 安全访问
index = array.size(arr) - 1
value = index >= 0 ? array.get(arr, index) : na
```

### 5. **内存泄漏**
```pine
// ❌ 无限增长
var float[] data = array.new<float>()
array.push(data, close)  // 永不清理

// ✅ 限制大小
if array.size(data) > 100
    array.shift(data)
```

### 6. **条件顺序错误**
```pine
// ❌ 第二个条件永远不执行
if close > ma50
    // 代码
else if close > ma20  // 永远false
    // 代码
```

### 7. **忽略na值**
```pine
// ❌ na值传播
result = (naValue + 10) / 2  // 结果是na

// ✅ 处理na值
result = (nz(naValue, 0) + 10) / 2
```

### 8. **性能陷阱**
```pine
// ❌ 重复计算
for i = 0 to 100
    ma = ta.sma(close, 20)  // 每次都计算

// ✅ 预计算
ma = ta.sma(close, 20)
for i = 0 to 100
    // 使用ma
```

### 9. **状态不同步**
```pine
// ❌ 多个状态变量
inLong1 = strategy.position_size > 0
inLong2 = someOtherCondition  // 可能不一致

// ✅ 单一状态
inLong = strategy.position_size > 0
```

### 10. **时间框架混淆**
```pine
// ❌ 错误认为这是小时数据
h1Trend = close > ta.sma(close, 50)  // 实际是当前时间框架

// ✅ 明确获取
h1Trend = request.security(..., "60", close) > request.security(..., "60", ta.sma(close, 50))
```

## 🛡️ 防错原则

### 1. **防御性编程**
```pine
// 总是检查边界
if index >= 0 and index < array.size(arr)
    value = array.get(arr, index)
```

### 2. **明确性原则**
```pine
// 使用括号明确运算顺序
condition = (rsi > 50 and close > ma) or volume > avgVolume
```

### 3. **单一职责**
```pine
// 每个变量/函数只做一件事
var bool inPosition = strategy.position_size > 0  // 状态跟踪
```

### 4. **最小化原则**
```pine
// 只在需要时计算
if showIndicator
    expensiveCalculation()
```

### 5. **一致性原则**
```pine
// 保持命名和风格一致
ma20 = ta.sma(close, 20)
ma50 = ta.sma(close, 50)  // 一致的命名
```

## 📝 代码审查清单

### ✅ 提交前检查

1. **重绘检查**
   - [ ] request.security() 是否有偏移？
   - [ ] 是否等待 barstate.isconfirmed？
   - [ ] 是否使用了 timenow 进行历史判断？

2. **性能检查**
   - [ ] 循环是否有重复计算？
   - [ ] 数组是否会无限增长？
   - [ ] request.security() 调用是否合理？

3. **逻辑检查**
   - [ ] 条件顺序是否正确？
   - [ ] 状态是否一致？
   - [ ] 是否处理了所有边界情况？

4. **类型检查**
   - [ ] 是否有类型转换？
   - [ ] 数组类型是否一致？
   - [ ] 是否处理了 na 值？

5. **测试检查**
   - [ ] 在不同时间框架测试了吗？
   - [ ] 历史数据表现如何？
   - [ ] 实时表现是否符合预期？

## 🎯 快速修复模板

### 修复重绘
```pine
// 添加偏移
value[1]

// 添加确认
if condition and barstate.isconfirmed

// 设置lookahead
request.security(..., lookahead=barmerge.lookahead_on)
```

### 修复性能
```pine
// 缓存计算
var cachedValue = na
if updateCondition
    cachedValue := expensiveCalculation()

// 限制数组
if array.size(arr) > maxSize
    array.shift(arr)
```

### 修复逻辑
```pine
// 使用括号
condition = (a and b) or (c and d)

// 处理na
if not na(value)
    // 使用value
```

## 💡 记住这些

1. **如果回测太完美，一定有重绘问题**
2. **性能问题往往来自循环和数组**
3. **逻辑错误最难发现，多测试**
4. **类型错误最容易，编译器会帮你**
5. **好的代码 = 简单 + 清晰 + 可测试**

## 🚀 进阶建议

1. **使用版本控制**
   - 每个重大修改提交
   - 可以回滚到工作版本

2. **编写测试用例**
   - 正常情况
   - 边界情况
   - 异常情况

3. **添加注释**
   ```pine
   // 为什么这样做，而不是做什么
   // 使用偏移避免未来泄漏
   dailyClose = request.security(..., close[1])
   ```

4. **模块化代码**
   - 每个函数一个职责
   - 可复用的功能提取出来

5. **持续学习**
   - 查看他人的代码
   - 学习最佳实践
   - 保持更新知识

---

**最终建议**：代码不仅要能运行，更要正确、高效、可维护。多思考，多测试，多改进！