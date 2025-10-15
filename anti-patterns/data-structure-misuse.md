# 数据结构误用反例

Pine Script v6 提供了 arrays、maps 和 matrices 等数据结构，误用这些结构会导致错误和性能问题。

## 1. 数组越界错误

### ❌ 错误示例：数组索引越界
```pine
//@version=6
indicator("错误：数组越界")

// ❌ 尝试访问不存在的索引
var float[] prices = array.new<float>()
array.push(prices, close)
array.push(prices, close[1])

// 错误：数组只有2个元素，但试图访问索引5
value = array.get(prices, 5)  // 运行时错误！
plot(value)
```

### 🚨 问题说明
- Pine Script 数组是 0 索引的
- 访问超出 `size - 1` 的索引会导致运行时错误
- 错误会导致脚本停止工作

### ✅ 正确做法：检查索引有效性
```pine
//@version=6
indicator("正确：检查索引")

var float[] prices = array.new<float>()
array.push(prices, close)
array.push(prices, close[1])

// ✅ 检查索引是否有效
index = 5
value = index < array.size(prices) ? array.get(prices, index) : na
plot(value, title="值", display=display.data_window)
```

## 2. 类型不匹配

### ❌ 错误示例：混合类型数组
```pine
//@version=6
indicator("错误：类型不匹配")

// ❌ 声明为float数组但试图插入int
var float[] mixedArray = array.new<float>()

array.push(mixedArray, close)      // OK，float
array.push(mixedArray, 10)        // OK，int可以自动转为float
array.push(mixedArray, "text")    // 错误！不能插入string
```

### 🚨 问题说明
- Pine Script 数组只能存储一种类型
- 类型在声明时确定
- 尝试插入不兼容类型会导致编译错误

### ✅ 正确做法：统一类型或使用不同数组
```pine
//@version=6
indicator("正确：统一类型")

// ✅ 方法1：统一使用float
var float[] numbers = array.new<float>()
array.push(numbers, close)
array.push(numbers, 10.0)  // 显式转换为float

// ✅ 方法2：为不同类型创建不同数组
var string[] texts = array.new<string>()
var float[] values = array.new<float>()

array.push(texts, "价格")
array.push(values, close)
```

## 3. 数组修改时遍历

### ❌ 错误示例：遍历时修改数组
```pine
//@version=6
indicator("错误：遍历时修改")

var float[] data = array.from(1, 2, 3, 4, 5)

// ❌ 遍历时添加元素，导致无限循环
for i = 0 to array.size(data) - 1
    value = array.get(data, i)
    if value > 3
        array.push(data, value * 2)  // 危险！数组在增长
```

### 🚨 问题说明
- 遍历时修改数组大小会导致未定义行为
- 可能导致无限循环或跳过元素
- Pine Script 可能限制循环次数（100次）

### ✅ 正确做法：使用临时数组
```pine
//@version=6
indicator("正确：使用临时数组")

var float[] data = array.from(1, 2, 3, 4, 5)
var float[] newData = array.new<float>()

// ✅ 收集需要添加的元素
for i = 0 to array.size(data) - 1
    value = array.get(data, i)
    if value > 3
        array.push(newData, value * 2)

// 遍历完成后合并
for i = 0 to array.size(newData) - 1
    array.push(data, array.get(newData, i))
```

## 4. Map 键类型错误

### ❌ 错误示例：使用错误类型的键
```pine
//@version=6
indicator("错误：Map键类型错误")

// ❌ Map只能使用string或int作为键
var map<float, string> wrongMap = map.new<float, string>()
map.put(wrongMap, 1.5, "value")  // 错误！float不能作为键

// ❌ 尝试使用bool作为键
var map<bool, float> boolMap = map.new<bool, float>()
map.put(boolMap, true, 100.0)     // 错误！bool不能作为键
```

### 🚨 问题说明
- Pine Script v6 的 Map 只支持 `string` 和 `int` 作为键
- 这是 Pine Script 的限制
- 使用其他类型会导致编译错误

### ✅ 正确做法：使用支持的键类型
```pine
//@version=6
indicator("正确：支持的键类型")

// ✅ 使用string作为键
var map<string, float> config = map.new<string, float>()
map.put(config, "risk", 2.0)
map.put(config, "reward", 4.0)

// ✅ 使用int作为键
var map<int, string> levels = map.new<int, string>()
map.put(levels, 1, "支撑")
map.put(levels, 2, "阻力")

// 如果需要其他类型，转换为string
key = str.tostring(someValue)
```

## 5. Matrix 维度不匹配

### ❌ 错误示例：矩阵运算维度错误
```pine
//@version=6
indicator("错误：矩阵维度错误")

// 创建不同维度的矩阵
m1 = matrix.new<float>(2, 3)  // 2行3列
m2 = matrix.new<float>(4, 5)  // 4行5列

// ❌ 尝试相乘不同维度
result = matrix.mult(m1, m2)  // 错误！维度不匹配

// ❌ 设置元素时越界
matrix.set(m1, 5, 5, 100.0)  // 错误！索引超出范围
```

### 🚨 问题说明
- 矩阵乘法要求第一个矩阵的列数等于第二个矩阵的行数
- 访问矩阵元素时必须在有效范围内
- 维度错误会导致运行时错误

### ✅ 正确做法：匹配维度
```pine
//@version=6
indicator("正确：矩阵维度匹配")

// ✅ 创建匹配维度的矩阵
m1 = matrix.new<float>(2, 3)  // 2行3列
m2 = matrix.new<float>(3, 4)  // 3行4列

// 可以相乘：3列 = 3行
result = matrix.mult(m1, m2)  // 结果是2行4列

// ✅ 安全设置元素
rows = matrix.rows(m1)
cols = matrix.columns(m1)
if rows > 0 and cols > 0
    matrix.set(m1, 0, 0, 100.0)  // 安全访问
```

## 6. 低效的数组操作

### ❌ 错误示例：频繁的数组操作
```pine
//@version=6
indicator("错误：低效数组操作")

var float[] data = array.new<float>()

// ❌ 在数组开头频繁插入（O(n)操作）
for i = 0 to 100
    array.unshift(data, close[i])  // 每次需要移动所有元素

// ❌ 频繁删除中间元素
for i = 50 to 60
    array.remove(data, i)  // 每次需要移动后续元素
```

### 🚨 问题说明
- `array.unshift()` 在开头插入需要移动所有元素
- `array.remove()` 删除中间元素需要移动后续元素
- 频繁执行这些操作性能很差

### ✅ 正确做法：选择合适的操作
```pine
//@version=6
indicator("正确：高效数组操作")

var float[] data = array.new<float>()

// ✅ 使用push在末尾添加（O(1)操作）
for i = 0 to 100
    array.push(data, close[i])

// ✅ 如果需要反转，之后一次性操作
if array.size(data) > 0
    array.reverse(data)

// ✅ 批量删除而不是逐个删除
if array.size(data) > 50
    data = array.slice(data, 0, 50)
```

## 7. Map 的误用

### ❌ 错误示例：Map用于简单列表
```pine
//@version=6
indicator("错误：Map误用")

// ❌ 使用Map存储简单序列
var map<string, float> priceMap = map.new<string, float>()
map.put(priceMap, "0", close[0])
map.put(priceMap, "1", close[1])
map.put(priceMap, "2", close[2])

// 访问时需要字符串转换，效率低
for i = 0 to 2
    price = map.get(priceMap, str.tostring(i))
```

### 🚨 问题说明
- Map 适用于键值对查找
- 对于简单的索引序列，Array更合适
- Map 的字符串键操作比数组索引慢

### ✅ 正确做法：选择合适的数据结构
```pine
//@version=6
indicator("正确：选择合适结构")

// ✅ 简单序列使用数组
var float[] prices = array.new<float>()
array.push(prices, close)
array.push(prices, close[1])
array.push(prices, close[2])

// ✅ Map用于真正需要键值查找的场景
var map<string, float> config = map.new<string, float>()
map.put(config, "stopLoss", 2.0)
map.put(config, "takeProfit", 4.0)
stopLoss = map.get(config, "stopLoss")
```

## 8. Matrix 用于简单数据

### ❌ 错误示例：过度使用Matrix
```pine
//@version=6
indicator("错误：过度使用Matrix")

// ❌ 只需要存储几个值却使用矩阵
data = matrix.new<float>(1, 5)
matrix.set(data, 0, 0, close)
matrix.set(data, 0, 1, high)
matrix.set(data, 0, 2, low)
matrix.set(data, 0, 3, open)
matrix.set(data, 0, 4, volume)

// 访问复杂
closeValue = matrix.get(data, 0, 0)
```

### 🚨 问题说明
- Matrix 适用于二维数学运算
- 简单数据使用Matrix过于复杂
- 访问和操作都不如数组直观

### ✅ 正确做法：使用数组或多个变量
```pine
//@version=6
indicator("正确：简单结构")

// ✅ 方法1：使用数组
var float[] ohlcv = array.new<float>()
array.push(ohlcv, close)
array.push(ohlcv, high)
array.push(ohlcv, low)
array.push(ohlcv, open)
array.push(ohlcv, volume)

// ✅ 方法2：使用结构化方法（如果数据相关）
type OHLCV
    float close
    float high
    float low
    float open
    float volume

data = OHLCV.new(close, high, low, open, volume)
```

## 9. 忽略类型检查

### ❌ 错误示例：不检查类型转换
```pine
//@version=6
indicator("错误：忽略类型检查")

// ❌ 可能失败的转换
strValue = "123.45"
numValue = float(strValue)  // 如果strValue不是有效数字会出错

// ❌ 不检查na值
value = someCalculation()
result = value * 2  // 如果value是na会导致错误
```

### 🚨 问题说明
- Pine Script 不会自动处理所有类型转换错误
- na 值参与运算会产生错误结果
- 需要显式检查和处理

### ✅ 正确做法：类型安全和na检查
```pine
//@version=6
indicator("正确：类型安全")

// ✅ 安全的字符串转换
strValue = "123.45"
numValue = str.tonumber(strValue)
result = na(numValue) ? 0.0 : numValue

// ✅ na值检查
value = someCalculation()
if not na(value)
    result = value * 2
else
    result = 0.0

// ✅ 使用nz函数
result = nz(value, 0.0) * 2
```

## 10. 数组/Map/Matrix 选择错误

### ❌ 错误示例：选择错误的数据结构
```pine
//@version=6
indicator("错误：结构选择错误")

// ❌ 需要快速查找却使用数组
var float[] searchArray = array.from(10, 20, 30, 40, 50)
target = 30
found = false
for i = 0 to array.size(searchArray) - 1  // O(n)查找
    if array.get(searchArray, i) == target
        found := true
        break
```

### 🚨 问题说明
- 数组查找是 O(n) 复杂度
- Map 查找是 O(1) 复杂度
- 选择错误的结构会影响性能

### ✅ 正确做法：根据需求选择
```pine
//@version=6
indicator("正确：结构选择")

// ✅ 需要快速查找使用Map
var map<int, bool> lookupMap = map.new<int, bool>()
map.put(lookupMap, 10, true)
map.put(lookupMap, 20, true)
map.put(lookupMap, 30, true)

target = 30
found = map.contains(lookupMap, target)  // O(1)查找

// ✅ 需要顺序访问使用数组
var float[] sequence = array.from(10, 20, 30, 40, 50)
for i = 0 to array.size(sequence) - 1
    value = array.get(sequence, i)
    // 处理序列
```

## 数据结构选择指南

| 需求 | 最佳选择 | 替代方案 | 注意事项 |
|------|----------|----------|----------|
| 简单列表 | Array | - | 索引访问快 |
| 键值查找 | Map | Array (小数据量) | Map只支持string/int键 |
| 数学矩阵 | Matrix | Array of Arrays | 注意维度匹配 |
| 固定集合 | Array | Map | 预分配大小 |
| 动态增长 | Array | - | 限制最大大小 |
| 缓存数据 | Map/Array | - | 考虑清理策略 |

## 最佳实践总结

1. **始终检查边界**：数组访问前检查索引
2. **类型一致性**：保持数组类型一致
3. **选择合适的结构**：根据需求选择Array/Map/Matrix
4. **避免遍历时修改**：使用临时数组
5. **注意性能影响**：了解操作的复杂度
6. **处理na值**：使用nz()或显式检查
7. **预分配大小**：已知大小时预分配
8. **批量操作**：使用内置函数代替循环

记住：**选择正确的数据结构是高效代码的基础！**