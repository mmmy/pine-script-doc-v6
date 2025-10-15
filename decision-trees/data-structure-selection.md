# 数据结构选择决策树

## 📦 起始问题：我需要存储什么类型的数据？

```
┌─────────────────────────────────────────────────────┐
│   🗃️ Pine Script v6 数据结构选择指南                │
│   Arrays (v4+) | Maps (v6) | Matrices (v6)         │
└─────────────────────────────────────────────────────┘
    │
    └─ 📊 数据维度？
        │
        ├─ 一维数据（列表）
        │   └─ ➡️ **Array**
        │
        ├─ 键值对（字典）
        │   └─ ➡️ **Map**
        │
        ├─ 二维数据（表格/矩阵）
        │   └─ ➡️ **Matrix**
        │
        └─ 简单变量
            └─ ➡️ **基础变量**
```

## 📚 Arrays（一维列表）

```
┌─ 选择：Array - 一维数据集合
│
├─ 🎯 用途场景？
│   │
│   ├─ 存储历史数据
│   │   └─ ✅ **价格/指标序列**
│   │       ```pine
│   │       // 存储最近N根K线的收盘价
│   │       var float[] closePrices = array.new<float>(50)
│   │       if barstate.isconfirmed
│   │           array.unshift(closePrices, close)
│   │           if array.size(closePrices) > 50
│   │               array.pop(closePrices)
│   │       ```
│   │
│   ├─ 存储信号
│   │   └─ ✅ **买卖信号序列**
│   │       ```pine
│   │       // 记录所有信号
│   │       var int[] signals = array.new<int>()
│   │       if buySignal
│   │           array.push(signals, 1)
│   │       if sellSignal
│   │           array.push(signals, -1)
│   │       ```
│   │
│   ├─ 存储计算结果
│   │   └─ ✅ **中间计算值**
│   │       ```pine
│   │       // 存储多次计算结果
│   │       var float[] results = array.new<float>()
│   │       for i = 0 to 10
│   │           array.push(results, ta.rsi(close, i + 5))
│   │       ```
│   │
│   └─ 存储配置参数
│       └─ ✅ **动态参数列表**
│           ```pine
│           // 可配置的周期列表
│           periods = array.from(5, 10, 20, 50, 100, 200)
│           for period in periods
│               ma = ta.sma(close, period)
│               plot(ma)
│           ```
│
├─ 🔧 Array 操作
│   │
│   ├─ 创建和初始化
│   │   ```pine
│   │   // 空数组
│   │   arr = array.new<float>()
│   │
│   │   // 预分配大小
│   │   arr = array.new<float>(100)
│   │
│   │   // 从值创建
│   │   arr = array.from(1, 2, 3, 4, 5)
│   │
│   │   // 填充初始值
│   │   arr = array.new<float>(10, 0.0)
│   │   ```
│   │
│   ├─ 添加元素
│   │   ```pine
│   │   // 末尾添加
│   │   array.push(arr, value)
│   │
│   │   // 开头添加
│   │   array.unshift(arr, value)
│   │
│   │   // 指定位置插入
│   │   array.insert(arr, index, value)
│   │   ```
│   │
│   ├─ 访问和修改
│   │   ```pine
│   │   // 获取元素
│   │   value = array.get(arr, index)
│   │
│   │   // 设置元素
│   │   array.set(arr, index, value)
│   │
│   │   // 简化语法
│   │   value = arr[index]
│   │   arr[index] = value
│   │   ```
│   │
│   └─ 删除元素
│       ```pine
│       // 删除末尾
│       array.pop(arr)
│
│       // 删除开头
│       array.shift(arr)
│
│       // 删除指定位置
│       array.remove(arr, index)
│
│       // 清空数组
│       array.clear(arr)
│       ```
│
├─ 📊 Array 实用函数
│   │
│   ├─ 查找和筛选
│   │   ```pine
│   │   // 查找元素
│   │   index = array.indexof(arr, targetValue)
│   │
│   │   // 检查包含
│   │   contains = array.includes(arr, targetValue)
│   │
│   │   // 筛选（Pine Script v6）
│   │   filtered = array.filter(arr, val => val > threshold)
│   │   ```
│   │
│   ├─ 统计计算
│   │   ```pine
│   │   // 求和
│   │   sum = array.sum(arr)
│   │
│   │   // 平均值
│   │   avg = array.avg(arr)
│   │
│   │   // 最大值/最小值
│   │   max = array.max(arr)
│   │   min = array.min(arr)
│   │
│   │   // 中位数
│   │   median = array.median(arr)
│   │   ```
│   │
│   ├─ 排序
│   │   ```pine
│   │   // 升序排序
│   │   array.sort(arr, order.ascending)
│   │
│   │   // 降序排序
│   │   array.sort(arr, order.descending)
│   │   ```
│   │
│   └─ 切片和合并
│       ```pine
│       // 切片
│       subArray = array.slice(arr, 0, 10)
│
│       // 合并
│       combined = array.concat(arr1, arr2)
│       ```
│
└─ ⚠️ Array 性能注意事项
    ├─ 大小限制
    │   - 最大 100,000 个元素
    │   - 合理使用，避免过大数组
    │
    ├─ 类型一致性
    │   - 数组只能存储一种类型
    │   - 声明时确定类型
    │
    └─ 循环优化
        ```pine
        // ❌ 低效
        result = 0.0
        for i = 0 to array.size(arr) - 1
            result += array.get(arr, i)

        // ✅ 高效
        result = array.sum(arr)
        ```
```

## 🗺️ Maps（键值对）- Pine Script v6

```
┌─ 选择：Map - 键值对存储
│
├─ 🎯 使用场景？
│   │
│   ├─ 配置管理
│   │   └─ ✅ **参数配置字典**
│   │       ```pine
│   │       // 策略参数配置
│   │       var map<string, float> config = map.new<string, float>()
│   │       if na(map.get(config, "risk"))
│   │           map.put(config, "risk", 2.0)
│   │           map.put(config, "reward", 4.0)
│   │           map.put(config, "maxDrawdown", 10.0)
│   │       ```
│   │
│   ├─ 缓存计算结果
│   │   └─ ✅ **计算缓存**
│   │       ```pine
│   │       // 缓存RSI计算结果
│   │       var map<string, float> rsiCache = map.new<string, float>()
│   │       cacheKey = str.tostring(bar_index) + "_" + str.tostring(rsiLength)
│   │       cachedRSI = map.get(rsiCache, cacheKey)
│   │       if na(cachedRSI)
│   │           cachedRSI := ta.rsi(close, rsiLength)
│   │           map.put(rsiCache, cacheKey, cachedRSI)
│   │       ```
│   │
│   ├─ 数据聚合
│   │   └─ ✅ **统计数据**
│   │       ```pine
│   │       // 按时间段聚合数据
│   │       var map<string, int> volumeByHour = map.new<string, int>()
│   │       hourKey = str.tostring(hour(time))
│   │       currentVol = map.get(volumeByHour, hourKey)
│   │       map.put(volumeByHour, hourKey, nz(currentVol) + volume)
│   │       ```
│   │
│   └─ 状态管理
│       └─ ✅ **状态追踪**
│           ```pine
│           // 追踪不同状态
│           var map<string, bool> states = map.new<string, bool>()
│           map.put(states, "inPosition", strategy.position_size != 0)
│           map.put(states, "trendUp", close > ta.sma(close, 20))
│           ```
│
├─ 🔧 Map 操作
│   │
│   ├─ 创建和初始化
│   │   ```pine
│   │   // 空map
│   │   m = map.new<string, int>()
│   │
│   │   // 带初始值
│   │   m = map.new<string, float>()
│   │   map.put(m, "key1", 1.0)
│   │   map.put(m, "key2", 2.0)
│   │   ```
│   │
│   ├─ 添加和更新
│   │   ```pine
│   │   // 添加键值对
│   │   map.put(m, "newKey", newValue)
│   │
│   │   // 批量添加
│   │   for [key, value] in [["a", 1], ["b", 2], ["c", 3]]
│   │       map.put(m, key, value)
│   │   ```
│   │
│   ├─ 访问数据
│   │   ```pine
│   │   // 获取值
│   │   value = map.get(m, "key")
│   │
│   │   // 带默认值
│   │   value = map.get(m, "key", defaultValue)
│   │
│   │   // 检查键是否存在
│   │   exists = map.contains(m, "key")
│   │   ```
│   │
│   └─ 删除和清空
│       ```pine
│       // 删除键
│       map.remove(m, "key")
│
│       // 获取所有键
│       keys = map.keys(m)
│
│       // 获取所有值
│       values = map.values(m)
│
│       // 清空map
│       map.clear(m)
│       ```
│
├─ 📊 Map 高级用法
│   │
│   ├─ 嵌套 Map
│   │   ```pine
│   │   // 二维数据结构
│   │   var map<string, map<string, float>> nested = map.new()
│   │   innerMap = map.new<string, float>()
│   │   map.put(innerMap, "value", 100.0)
│   │   map.put(nested, "outer", innerMap)
│   │   ```
│   │
│   ├─ Map 作为缓存
│   │   ```pine
│   │   // LRU缓存实现
│   │   var map<string, int> cache = map.new<string, int>()
│   │   var int[] accessOrder = array.new<int>()
│   │
│   │   // 缓存管理逻辑
│   │   if array.size(accessOrder) > 100
│   │       oldKey = array.shift(accessOrder)
│   │       map.remove(cache, oldKey)
│   │   ```
│   │
│   └─ 动态配置
│       ```pine
│       // 动态读取配置
│       configMap = map.from([
│           ["period", 20],
│           ["deviation", 2.0],
│           ["showBands", true]
│       ])
│       ```
│
└─ ⚠️ Map 限制
    ├─ 键类型限制
    │   - 只支持 string 和 int 类型作为键
    │   - 值可以是任何类型
    │
    ├─ 性能考虑
    │   - 查找速度快 O(1)
    │   - 适合大量键值对
    │
    └─ 内存使用
        - 比数组占用更多内存
        - 合理控制map大小
```

## 🔢 Matrices（矩阵）- Pine Script v6

```
┌─ 选择：Matrix - 二维数据
│
├─ 🎯 使用场景？
│   │
│   ├─ 数学计算
│   │   └─ ✅ **线性代数运算**
│   │       ```pine
│   │       // 创建矩阵
│   │       m = matrix.new<float>(3, 3, 0.0)
│   │
│   │       // 填充数据
│   │       for i = 0 to 2
│   │           for j = 0 to 2
│   │               matrix.set(m, i, j, i + j)
│   │
│   │       // 矩阵运算
│   │       identity = matrix.identity(3)
│   │       result = matrix.mult(m, identity)
│   │       ```
│   │
│   ├─ 数据网格
│   │   └─ ✅ **二维数据存储**
│   │       ```pine
│   │       // 价格网格
│   │       priceGrid = matrix.new<float>(10, 10, 0.0)
│   │
│   │       // 填充价格数据
│   │       basePrice = close
│   │       for i = 0 to 9
│   │           for j = 0 to 9
│   │               price = basePrice * (1 + i * 0.01) * (1 + j * 0.01)
│   │               matrix.set(priceGrid, i, j, price)
│   │       ```
│   │
│   ├─ 相关性矩阵
│   │   └─ ✅ **资产相关性**
│   │       ```pine
│   │       // 多资产相关性矩阵
│   │       corrMatrix = matrix.new<float>(5, 5, 0.0)
│   │
│   │       // 计算相关性
│   │       assets = array.from("AAPL", "GOOGL", "MSFT", "AMZN", "FB")
│   │       for i = 0 to 4
│   │           for j = 0 to 4
│   │               corr = ta.correlation(returns[i], returns[j], 20)
│   │               matrix.set(corrMatrix, i, j, corr)
│   │       ```
│   │
│   └─ 机器学习数据
│       └─ ✅ **特征矩阵**
│           ```pine
│           // 特征数据矩阵
│           features = matrix.new<float>(100, 5, 0.0)
│
│           // 填充特征：RSI, MACD, MA差等
│           for i = 0 to 99
│               matrix.set(features, i, 0, ta.rsi(close[i], 14))
│               matrix.set(features, i, 1, ta.macd(close[i])[0])
│               matrix.set(features, i, 2, close[i] - ta.sma(close[i], 20))
│           ```
│
├─ 🔧 Matrix 操作
│   │
│   ├─ 基础操作
│   │   ```pine
│   │   // 创建矩阵
│   │   m = matrix.new<int>(rows, cols, initialValue)
│   │
│   │   // 获取元素
│   │   value = matrix.get(m, row, col)
│   │
│   │   // 设置元素
│   │   matrix.set(m, row, col, value)
│   │
│   │   // 获取维度
│   │   rows = matrix.rows(m)
│   │   cols = matrix.columns(m)
│   │   ```
│   │
│   ├─ 矩阵运算
│   │   ```pine
│   │   // 加法
│   │   result = matrix.add(m1, m2)
│   │
│   │   // 减法
│   │   result = matrix.sub(m1, m2)
│   │
│   │   // 乘法
│   │   result = matrix.mult(m1, m2)
│   │
│   │   // 数量积
│   │   result = matrix.dot(m1, m2)
│   │
│   │   // 转置
│   │   transposed = matrix.transpose(m)
│   │   ```
│   │
│   ├─ 特殊矩阵
│   │   ```pine
│   │   // 单位矩阵
│   │   identity = matrix.identity(size)
│   │
│   │   // 零矩阵
│   │   zeros = matrix.new<float>(rows, cols, 0.0)
│   │
│   │   // 对角矩阵
│   │       diagonal = matrix.diagonal(array.from(1, 2, 3, 4))
│   │   ```
│   │
│   └─ 高级运算
│       ```pine
│       // 行列式
│       det = matrix.det(m)

│       // 逆矩阵
│       inverse = matrix.inv(m)

│       // 伪逆
│       pseudoInv = matrix.pinv(m)

│       // 特征值（需要库）
│       ```
│
├─ 📊 Matrix 实用技巧
│   │
│   ├─ 数据转换
│   │   ```pine
│   │   // Array转Matrix
│   │   arr = array.from(1, 2, 3, 4, 5, 6)
│   │   m = matrix.from_array(arr, 2, 3)  // 2行3列
│   │
│   │   // Matrix转Array
│   │   flatArr = matrix.to_array(m)
│   │   ```
│   │
│   ├─ 行列操作
│   │   ```pine
│   │   // 获取行
│   │   row = matrix.row(m, rowIndex)

│   │   // 获取列
│   │   col = matrix.col(m, colIndex)

│   │   // 设置行
│   │   matrix.set_row(m, rowIndex, newRowArray)

│   │   // 设置列
│   │   matrix.set_col(m, colIndex, newColArray)
│   │   ```
│   │
│   └─ 子矩阵
│       ```pine
│       // 提取子矩阵
│       subM = matrix.submatrix(m, startRow, endRow, startCol, endCol)

│       // 合并矩阵
│       combined = matrix.concat_vert(m1, m2)  // 垂直合并
│       combined = matrix.concat_horiz(m1, m2)  // 水平合并
│       ```
│
└─ ⚠️ Matrix 限制
    ├─ 维度限制
    │   - 最大维度受内存限制
    │   - 合理控制矩阵大小
    │
    ├─ 计算复杂度
    │   - 矩阵乘法 O(n³)
    │   - 注意性能影响
    │
    └─ 数据类型
        - 所有元素必须是相同类型
        - 支持 int, float, bool
```

## 🔄 数据结构比较和选择

```
┌─ 数据结构选择指南
│
├─ 📊 根据数据维度选择
│   │
│   ├─ 一维列表 → Array
│   │   - 时间序列数据
│   │   - 简单值集合
│   │   - 历史价格存储
│   │
│   ├─ 键值对 → Map
│   │   - 配置参数
│   │   - 缓存系统
│   │   - 字典数据
│   │
│   └─ 二维表格 → Matrix
│       - 数学运算
│       - 网格数据
│       - 特征矩阵
│
├─ ⚡ 根据性能需求选择
│   │
│   ├─ 快速查找 → Map
│   │   - O(1) 查找时间
│   │   - 大量键值对
│   │
│   ├─ 顺序访问 → Array
│   │   - O(1) 索引访问
│   │   - 遍历操作
│   │
│   └─ 数学运算 → Matrix
│       - 线性代数
│       - 批量计算
│
├─ 💾 根据内存使用选择
│   │
│   ├─ 内存效率 → Array
│   │   - 最小内存占用
│   │   - 简单数据
│   │
│   ├─ 功能灵活 → Map
│   │   - 动态键值
│   │   - 元数据存储
│   │
│   └─ 结构化数据 → Matrix
│       - 二维数据
│       - 表格结构
│
└─ 🔄 互转操作
    ├─ Array ↔ Map
    │   ```pine
    │   // Array转Map
    │   arr = array.from(1, 2, 3)
    │   m = map.new<string, int>()
    │   for i = 0 to array.size(arr) - 1
    │     map.put(m, "key" + str.tostring(i), arr[i])
    │   ```
    │
    ├─ Array ↔ Matrix
    │   ```pine
    │   // 一维Array转Matrix
    │   m = matrix.from_array(arr, rows, cols)
    │
    │   // Matrix转Array
    │   arr = matrix.to_array(m)
    │   ```
    │
    └─ Map → Array
        ```pine
        // Map的键转Array
        keys = map.keys(m)

        // Map的值转Array
        values = map.values(m)
        ```
```

## 📝 最佳实践总结

### Array 最佳实践
```pine
// 1. 预分配大小
var float[] prices = array.new<float>(100, 0.0)

// 2. 使用内置函数
sum = array.sum(arr)  // 而不是手动循环

// 3. 批量操作
array.fill(arr, value)  // 批量填充

// 4. 类型安全
var int[] numbers = array.new<int>()  // 明确类型
```

### Map 最佳实践
```pine
// 1. 使用描述性键
map.put(config, "stopLossPercent", 2.0)

// 2. 检查键存在
if map.contains(cache, key)
    value = map.get(cache, key)

// 3. 使用默认值
value = map.get(m, "key", defaultValue)

// 4. 缓存管理
if map.size(cache) > maxCacheSize
    map.clear(cache)
```

### Matrix 最佳实践
```pine
// 1. 预先计算维度
rows = math.ceil(math.sqrt(dataSize))
cols = math.ceil(dataSize / rows)

// 2. 使用矩阵运算
result = matrix.mult(m1, m2)  // 而不是嵌套循环

// 3. 特殊矩阵
identity = matrix.identity(size)  // 使用内置函数

// 4. 内存管理
if matrix.rows(m) > maxRows
    m = matrix.submatrix(m, 0, maxRows, 0, matrix.columns(m))
```

## ⚠️ 常见错误

1. **Array 索引越界**
   ```pine
   // ❌ 错误
   value = arr[array.size(arr)]  // 最后一个索引是 size-1

   // ✅ 正确
   value = arr[array.size(arr) - 1]
   ```

2. **Map 类型错误**
   ```pine
   // ❌ 错误：float不能作为键
   m = map.new<float, string>()

   // ✅ 正确
   m = map.new<string, float>()
   ```

3. **Matrix 维度不匹配**
   ```pine
   // ❌ 错误：维度不匹配
   result = matrix.mult(m2x3, m4x5)

   // ✅ 正确
   result = matrix.mult(m2x3, m3x5)
   ```

4. **内存泄漏**
   ```pine
   // ❌ 错误：无限增长
   array.push(arr, value)  // 从不清理

   // ✅ 正确：限制大小
   if array.size(arr) > maxSize
       array.shift(arr)
   ```

## 🎯 快速决策表

| 需求 | Array | Map | Matrix |
|------|-------|-----|---------|
| 时间序列数据 | ✅ | ❌ | ❌ |
| 键值查找 | ❌ | ✅ | ❌ |
| 数学矩阵运算 | ❌ | ❌ | ✅ |
| 简单值列表 | ✅ | ❌ | ❌ |
| 配置参数 | ❌ | ✅ | ❌ |
| 二维数据网格 | 可以 | 可以 | ✅ |
| 缓存系统 | ❌ | ✅ | ❌ |
| 性能（查找） | O(n) | O(1) | O(n·m) |
| 内存效率 | 高 | 中 | 低 |

选择数据结构的关键是：**匹配数据特性，优化访问模式，考虑性能限制**。