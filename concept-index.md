# Pine Script v6 概念索引

## 目录
- [核心概念](#核心概念)
- [语言特性](#语言特性)
- [数据类型](#数据类型)
- [内置函数](#内置函数)
- [脚本类型](#脚本类型)
- [可视化](#可视化)
- [高级功能](#高级功能)
- [常见问题](#常见问题)

---

## 核心概念

### A
- **Alerts (警报)** - [📖 文档](pine-script-docs/concepts/alerts.md) | [❌ 反例](anti-patterns/alert-mistakes.md) | [🌳 决策树](decision-trees/alert-implementation.md)
- **Arrays (数组)** - [📖 文档](pine-script-docs/language/arrays.md) | [❌ 反例](anti-patterns/data-structure-misuse.md) | [🌳 决策树](decision-trees/data-structure-selection.md)
- **Annotations (注释)** - [📖 文档](pine-script-reference/Annotations.md)

### B
- **Bar States (K线状态)** - [📖 文档](pine-script-docs/concepts/bar-states.md)
- **Built-ins (内置变量)** - [📖 文档](pine-script-docs/language/built-ins.md)

### C
- **Chart Information (图表信息)** - [📖 文档](pine-script-docs/concepts/chart-information.md)
- **Conditional Structures (条件结构)** - [📖 文档](pine-script-docs/language/conditional-structures.md) | [❌ 反例](anti-patterns/logic-errors.md)
- **Constants (常量)** - [📖 文档](pine-script-reference/Constants.md)
- **Concepts (概念)** - [📖 文档](pine-script-docs/concepts/)

### D
- **Data Structures (数据结构)** - [🌳 决策树](decision-trees/data-structure-selection.md) | [❌ 反例](anti-patterns/data-structure-misuse.md)

### E
- **Enums (枚举)** - [📖 文档](pine-script-docs/language/enums.md)
- **Execution Model (执行模型)** - [📖 文档](pine-script-docs/language/execution-model.md)

### F
- **Functions (函数)** - [📖 文档](pine-script-docs/language/user-defined-functions.md) | [📖 参考](pine-script-reference/Functions.md)

### I
- **Identifiers (标识符)** - [📖 文档](pine-script-docs/language/identifiers.md)
- **Inputs (输入参数)** - [📖 文档](pine-script-docs/concepts/inputs.md)
- **Indicator (指标)** - [🌳 决策树](decision-trees/script-type-selection.md)

### L
- **Language (语言)** - [📖 文档](pine-script-docs/language/)
- **Libraries (库)** - [📖 文档](pine-script-docs/concepts/libraries.md)
- **Loops (循环)** - [📖 文档](pine-script-docs/language/loops.md) | [❌ 反例](anti-patterns/performance-traps.md)

### M
- **Maps (映射)** - [🌳 决策树](decision-trees/data-structure-selection.md) | [❌ 反例](anti-patterns/data-structure-misuse.md)
- **Matrices (矩阵)** - [🌳 决策树](decision-trees/data-structure-selection.md) | [❌ 反例](anti-patterns/data-structure-misuse.md)
- **Methods (方法)** - [📖 文档](pine-script-docs/language/methods.md)

### O
- **Objects (对象)** - [📖 文档](pine-script-docs/language/objects.md)
- **Operators (运算符)** - [📖 文档](pine-script-docs/language/operators.md) | [📖 参考](pine-script-reference/Operators.md)

### P
- **Performance (性能)** - [❌ 反例](anti-patterns/performance-traps.md) | [🌳 决策树](decision-trees/performance-optimization.md)
- **Plotting (绘图)** - [📖 文档](pine-script-docs/visuals/plots.md) | [🌳 决策树](decision-trees/visualization-selection.md)
- **Properties (属性)** - [📖 文档](pine-script-docs/visuals/overview.md)

### R
- **Repainting (重绘)** - [📖 文档](pine-script-docs/concepts/repainting.md) | [❌ 反例](anti-patterns/repainting-errors.md) | [🌳 决策树](decision-trees/avoid-repainting.md)
- **Reference (参考)** - [📖 文档](pine-script-reference/)
- **Request Security (跨周期请求)** - [🌳 决策树](decision-trees/multi-timeframe.md) | [❌ 反例](anti-patterns/multi-timeframe-errors.md)

### S
- **Script Structure (脚本结构)** - [📖 文档](pine-script-docs/language/script-structure.md)
- **Sessions (交易时段)** - [📖 文档](pine-script-docs/concepts/sessions.md)
- **Strategies (策略)** - [📖 文档](pine-script-docs/concepts/strategies.md) | [🌳 决策树](decision-trees/script-type-selection.md) | [❌ 反例](anti-patterns/strategy-mistakes.md)
- **Strings (字符串)** - [📖 文档](pine-script-docs/concepts/strings.md)

### T
- **Time (时间)** - [📖 文档](pine-script-docs/concepts/time.md)
- **Timeframes (时间框架)** - [📖 文档](pine-script-docs/concepts/timeframes.md)
- **Type System (类型系统)** - [📖 文档](pine-script-docs/language/type-system.md) | [📖 参考](pine-script-reference/Types.md)

### V
- **Variable Declarations (变量声明)** - [📖 文档](pine-script-docs/language/variable-declarations.md) | [📖 参考](pine-script-reference/Variables.md)
- **Variables (变量)** - [📖 文档](pine-script-docs/language/variable-declarations.md)
- **Visuals (可视化)** - [📖 文档](pine-script-docs/visuals/) | [🌳 决策树](decision-trees/visualization-selection.md)

---

## 按类别快速查找

### 🔧 语言基础
- [执行模型](pine-script-docs/language/execution-model.md) - Pine Script 如何运行
- [类型系统](pine-script-docs/language/type-system.md) - 类型与限定符
- [脚本结构](pine-script-docs/language/script-structure.md) - 脚本组织
- [变量声明](pine-script-docs/language/variable-declarations.md) - var, varip, simple等
- [标识符](pine-script-docs/language/identifiers.md) - 命名规则

### 📊 数据处理
- [数组](pine-script-docs/language/arrays.md) - 一维数据集合
- [映射](knowledge-graph.json#maps) - 键值对存储 (v6)
- [矩阵](knowledge-graph.json#matrices) - 二维数据 (v6)
- [循环](pine-script-docs/language/loops.md) - 迭代处理
- [内置变量](pine-script-docs/language/built-ins.md) - open, high, low, close等

### 🎯 控制流
- [条件结构](pine-script-docs/language/conditional-structures.md) - if, switch
- [循环](pine-script-docs/language/loops.md) - for, while
- [运算符](pine-script-docs/language/operators.md) - 数学、比较、逻辑
- [函数](pine-script-docs/language/user-defined-functions.md) - 自定义函数

### 📈 脚本类型
- [指标](decision-trees/script-type-selection.md#indicator) - 分析工具
- [策略](decision-trees/script-type-selection.md#strategy) - 交易模拟
- [库](decision-trees/script-type-selection.md#library) - 代码复用

### 🎨 可视化
- [绘图](pine-script-docs/visuals/plots.md) - 基础绘图
- [背景](pine-script-docs/visuals/backgrounds.md) - 背景色
- [线条和框](pine-script-docs/visuals/lines-and-boxes.md) - 几何图形
- [表格](pine-script-docs/visuals/tables.md) - 数据表格
- [标签和形状](pine-script-docs/visuals/text-and-shapes.md) - 文本和图形

### ⚠️ 常见问题
- [重绘](anti-patterns/repainting-errors.md) - 避免重绘问题
- [性能](anti-patterns/performance-traps.md) - 优化脚本性能
- [逻辑错误](anti-patterns/logic-errors.md) - 避免逻辑陷阱
- [数据结构误用](anti-patterns/data-structure-misuse.md) - 正确使用数据结构

---

## 学习路径建议

### 🌱 初学者路径 (1-2周)
1. [脚本结构](pine-script-docs/language/script-structure.md) - 了解基础
2. [类型系统基础](pine-script-docs/language/type-system.md#types) - 基本类型
3. [变量声明](pine-script-docs/language/variable-declarations.md) - 存储数据
4. [条件结构](pine-script-docs/language/conditional-structures.md) - 控制逻辑
5. [内置变量](pine-script-docs/language/built-ins.md#built-in-variables) - 使用OHLCV
6. [基础绘图](pine-script-docs/visuals/plots.md) - 显示数据
7. [输入参数](pine-script-docs/concepts/inputs.md) - 用户交互
8. [创建第一个指标](decision-trees/script-type-selection.md#indicator) - 实践

### 🌿 中级路径 (2-4周)
1. [执行模型](pine-script-docs/language/execution-model.md) - 深入理解
2. [时间序列](pine-script-docs/language/execution-model.md#time-series) - 历史数据
3. [数组](pine-script-docs/language/arrays.md) - 数据集合
4. [函数](pine-script-docs/language/user-defined-functions.md) - 代码复用
5. [循环](pine-script-docs/language/loops.md) - 迭代计算
6. [警报](pine-script-docs/concepts/alerts.md) - 通知系统
7. [策略基础](pine-script-docs/concepts/strategies.md) - 交易逻辑
8. [避免重绘](decision-trees/avoid-repainting.md) - 代码稳定性

### 🌳 高级路径 (1-2月)
1. [类型系统进阶](pine-script-docs/language/type-system.md#qualifiers) - 理解限定符
2. [映射和矩阵](decision-trees/data-structure-selection.md) - v6新特性
3. [库开发](pine-script-docs/concepts/libraries.md) - 代码组织
4. [跨周期数据](decision-trees/multi-timeframe.md) - 多时间框架
5. [性能优化](decision-trees/performance-optimization.md) - 提升效率
6. [高级可视化](decision-trees/visualization-selection.md) - 专业图表
7. [反模式学习](anti-patterns/) - 避免错误
8. [知识图谱](knowledge-graph.json) - 概念关联

---

## 快速参考

### 🎯 常用函数速查

#### 技术指标
```pine
// 移动平均
ta.sma(source, length)
ta.ema(source, length)
ta.wma(source, length)

// RSI
ta.rsi(source, length)

// MACD
[macd, signal, hist] = ta.macd(source, 12, 26, 9)

// ATR
ta.atr(length)
```

#### 数组操作
```pine
// 创建
arr = array.new<float>(size, initialValue)
arr = array.from(val1, val2, val3)

// 添加
array.push(arr, value)
array.unshift(arr, value)

// 访问
value = array.get(arr, index)
value = arr[index]  // v6+

// 统计
sum = array.sum(arr)
avg = array.avg(arr)
max = array.max(arr)
```

#### 映射操作 (v6)
```pine
// 创建
m = map.new<string, float>()

// 添加
map.put(m, "key", value)

// 获取
value = map.get(m, "key", defaultValue)

// 检查
exists = map.contains(m, "key")
```

### ⚡ 性能提示

- ✅ 使用 `var` 缓存计算结果
- ✅ 限制数组大小
- ✅ 使用内置函数代替循环
- ✅ 缓存 `request.security()` 调用
- ❌ 避免深度嵌套循环
- ❌ 不要在循环中重复计算

### 🚨 重绘检查

- ✅ 使用 `[1]` 偏移历史数据
- ✅ 使用 `barstate.isconfirmed`
- ✅ 设置 `lookahead=barmerge.lookahead_on`
- ❌ 不要在实时K线使用 `close/high/low`
- ❌ 不要使用 `timenow` 进行历史判断

---

## 相关资源

### 📚 文档
- [官方文档](https://www.tradingview.com/pine-script-docs/)
- [函数参考](pine-script-reference/)
- [概念说明](pine-script-docs/)

### 🛠️ 工具
- [决策树](decision-trees/) - 做出最佳选择
- [反例库](anti-patterns/) - 避免常见错误
- [知识图谱](knowledge-graph.json) - 理解概念关系

### 💡 学习资源
- [示例代码](examples/) - 实用示例
- [最佳实践](common-mistakes-summary.md) - 编码规范
- [常见问题](常见问题.md) - FAQ

---

## 搜索提示

### 按功能搜索
- **绘图**: plot, plotshape, label, line
- **策略**: strategy.entry, strategy.exit, strategy.position_size
- **数据**: array, map, matrix, request.security
- **时间**: time, timenow, barstate.isconfirmed
- **类型**: int, float, string, bool, color

### 按问题搜索
- **重绘**: repainting, future leak, lookahead
- **性能**: performance, loop, calculation
- **错误**: error, na, runtime error
- **语法**: syntax, declaration, scope

---

*最后更新: 2025-10-13*
*版本: Pine Script v6*