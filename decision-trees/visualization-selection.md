# 可视化选择决策树

## 📊 起始问题：我需要显示什么类型的数据？

```
┌─────────────────────────────────────────────────────┐
│   🎨 选择合适的可视化方式来传达你的数据              │
└─────────────────────────────────────────────────────┘
    │
    └─ 📈 数据类型？
        │
        ├─ 连续数据（价格、指标值）
        │   └─ ➡️ **Plot 系列**
        │
        ├─ 离散事件（信号、标记）
        │   └─ ➡️ **Shapes/Labels**
        │
        ├─ 区域范围（支撑阻力、通道）
        │   └─ ➡️ **Lines/Fills/Boxes**
        │
        ├─ 结构化数据（表格、信息面板）
        │   └─ ➡️ **Tables/Backgrounds**
        │
        └─ 复杂组合（多元素组合）
            └─ ➡️ **混合方案**
```

## 📈 Plot 系列（连续数据）

```
┌─ 选择：Plot 系列
│
├─ 🎯 显示目的？
│   │
│   ├─ 单条曲线
│   │   └─ ✅ **基础 plot()**
│   │       ```pine
│   │       // 简单线条
│   │       plot(ta.sma(close, 20), "MA20", color.blue)
│   │       ```
│   │
│   ├─ 多条曲线
│   │   └─ ✅ **多个 plot()**
│   │       ```pine
│   │       // MA 组合
│   │       plot(ta.sma(close, 20), "MA20", color.blue)
│   │       plot(ta.sma(close, 50), "MA50", color.red)
│   │       plot(ta.sma(close, 200), "MA200", color.green)
│   │       ```
│   │
│   ├─ 填充区域
│   │   └─ ✅ **plot.style_area/histogram**
│   │       ```pine
│   │       // 面积图
│   │       plot(volume, "成交量",
│   │            style=plot.style_histogram,
│   │            color=volume > ta.sma(volume, 20) ? color.green : color.red)
│   │       ```
│   │
│   └─ 特殊样式
│       └─ ✅ **多种 plot style**
│           ```pine
│           // 柱状图
│           plot(rsi - 50, style=plot.style_columns)
│
│           // 阶梯线
│           plot(value, style=plot.style_stepline)
│
│           // 圆点标记
│           plot(value, style=plot.style_circles)
│           ```
│
├─ 🎨 样式定制
│   │
│   ├─ 颜色变化
│   │   ```pine
│   │   // 动态颜色
│   │   maColor = ma20 > ma50 ? color.green : color.red
│   │   plot(ma20, color=maColor)
│   │   ```
│   │
│   ├─ 线条样式
│   │   ```pine
│   │   plot(ma20,
│   │       linewidth=2,        // 线宽
│   │       style=plot.style_line,
│   │       trackprice=true)     // 水平线
│   │   ```
│   │
│   └─ 显示范围
│       ```pine
│       plot(ma20,
│           display=display.pane,     // 显示窗格
│           join=true)               // 连接na值
│       ```
│
└─ 📊 特殊应用
    ├─ 多数据系列
    │   ```pine
    │   // 使用 plotchar 显示多个值
    │   plotchar(series1, "系列1", "A", location.top)
    │   plotchar(series2, "系列2", "B", location.bottom)
    │   ```
    │
    ├─ 背景高亮
    │   ```pine
    │   // 背景着色
    │   bgcolor(rsi > 70 ? color.new(color.red, 90) : na)
    │   ```
    │
    └─ 价格标记
        ```pine
        // 在价格上标记
        plotshape(signal, style=shape.triangleup,
                 location=location.belowbar)
        ```
```

## 📍 Shapes/Labels（离散事件）

```
┌─ 选择：Shapes/Labels
│
├─ 🎯 事件类型？
│   │
│   ├─ 简单标记
│   │   └─ ✅ **plotshape()**
│   │       ```pine
│   │       // 买入信号
│   │       plotshape(buySignal,
│   │           title="买入",
│   │           style=shape.labelup,
│   │           location=location.belowbar,
│   │           color=color.green,
│   │           text="BUY")
│   │       ```
│   │
│   ├─ 自定义标签
│   │   └─ ✅ **label.new()**
│   │       ```pine
│   │       // 详细信息标签
│   │       if buySignal
│   │           label.new(bar_index, low,
│   │               text="买入\n价格: " + str.tostring(close),
│   │               color=color.green,
│   │               style=label.style_label_up,
│   │               size=size.small)
│   │       ```
│   │
│   └─ 多种形状
│       └─ ✅ **不同 shape.style**
│           ```pine
│           // 箭头
│           plotshape(upSignal, style=shape.triangleup)
│
│           // 圆圈
│           plotshape(level, style=shape.circle)
│
│           // 方块
│           plotshape(signal, style=shape.square)
│
│           // X标记
│           plotshape(error, style=shape.xcross)
│           ```
│
├─ 💡 位置控制
│   │
│   ├─ 相对位置
│   │   ```pine
│   │   // 相对K线的位置
│   │   location.abovebar    // K线上方
│   │   location.belowbar    // K线下方
│   │   location.absolute    // 绝对位置
│   │   location.top         // 顶部
│   │   location.bottom      // 底部
│   │   ```
│   │
│   ├─ 绝对位置
│   │   ```pine
│   │   // 指定具体价格位置
│   │   label.new(bar_index, 100.0, "水平线")
│   │   ```
│   │
│   └─ 偏移位置
│       ```pine
│       // 偏移位置
│       label.new(bar_index + 2, high, "未来标记")
│       ```
│
├─ 🎨 样式选项
│   │
│   ├─ 颜色和大小
│   │   ```pine
│   │   plotshape(signal,
│   │       color=color.blue,
│   │       size=size.normal,     // small/normal/large/huge
│   │       offset=0)             // 偏移
│   │   ```
│   │
│   ├─ 文本格式
│   │   ```pine
│   │   label.new(...,
│   │       textcolor=color.white,
│   │       fontfamily=font.family.default,
│   │       size=size.normal)
│   │   ```
│   │
│   └─ 显示控制
│       ```pine
│       // 条件显示
│       if showLabels and condition
│           label.new(...)
│
│       // 限制数量
│       var int labelCount = 0
│       if labelCount < 10
│           labelCount += 1
│           label.new(...)
│       ```
│
└─ 🔄 管理策略
    ├─ 清理旧标签
    │   ```pine
    │   // 保存标签引用
    │   var label[] labelArray = array.new<label>()
    │
    │   // 添加新标签
    │   if condition
    │       array.push(labelArray, label.new(...))
    │
    │   // 清理旧标签
    │   if array.size(labelArray) > 20
    │       label.delete(array.shift(labelArray))
    │   ```
    │
    └─ 更新标签
        ```pine
        // 更新现有标签
        var label myLabel = na
        if na(myLabel)
            myLabel := label.new(...)
        else
            label.set_text(myLabel, newText)
            label.set_color(myLabel, newColor)
        ```
```

## 📏 Lines/Fills/Boxes（区域范围）

```
┌─ 选择：Lines/Fills/Boxes
│
├─ 📐 需要绘制什么？
│   │
│   ├─ 水平/垂直线
│   │   └─ ✅ **hline/vline**
│   │       ```pine
│   │       // 水平线
│   │       hline(100, "阻力位", color.red, linestyle=hline.style_dashed)
│   │
│   │       // 垂直线
│   │       vline(bar_index, "时间标记", color.blue)
│   │       ```
│   │
│   ├─ 趋势线
│   │   └─ ✅ **line.new()**
│   │       ```pine
│   │       // 画趋势线
│   │       if trendStart
│   │           line.new(x1=bar_index[1], y1=high[1],
│   │                    x2=bar_index, y2=high,
│   │                    color=color.blue,
│   │                    width=2,
│   │                    style=line.style_solid,
│   │                    extend=extend.right)
│   │       ```
│   │
│   ├─ 填充区域
│   │   └─ ✅ **fill()**
│   │       ```pine
│   │       // 填充两条线之间
│   │       p1 = plot(ta.sma(close, 20))
│   │       p2 = plot(ta.sma(close, 50))
│   │       fill(p1, p2, color=color.new(color.blue, 90))
│   │       ```
│   │
│   └─ 矩形区域
│       └─ ✅ **box.new()**
│           ```pine
│           // 绘制矩形
│           if zoneStart
│               box.new(left=bar_index[10], top=high[10],
│                       right=bar_index, bottom=low,
│                       border_color=color.green,
│                       bgcolor=color.new(color.green, 90))
│           ```
│
├─ 🎨 样式定制
│   │
│   ├─ 线条样式
│   │   ```pine
│   │   line.style_solid      // 实线
│   │   line.style_dashed     // 虚线
│   │   line.style_dotted     // 点线
│   │   line.style_arrow_right  // 右箭头
│   │   ```
│   │
│   ├─ 扩展选项
│   │   ```pine
│   │   extend.none          // 不延伸
│   │   extend.right          // 向右延伸
│   │   extend.left          // 向左延伸
│   │   extend.both          // 双向延伸
│   │   ```
│   │
│   └─ 填充透明度
│       ```pine
│       // 控制透明度
│       fill(p1, p2, color=color.new(color.blue, 80))  // 80% 透明
│       ```
│
├─ 🔧 动态更新
│   │
│   ├─ 移动线条
│   │   ```pine
│   │   // 保存线条引用并更新
│   │   var line trendLine = na
│   │   if na(trendLine)
│   │       trendLine := line.new(...)
│   │   else
│   │       line.set_x2(trendLine, bar_index)
│   │       line.set_y2(trendLine, currentPrice)
│   │   ```
│   │
│   ├─ 删除对象
│   │   ```pine
│   │   // 清理线条
│   │   line.delete(oldLine)
│   │   box.delete(oldBox)
│   │   ```
│   │
│   └─ 批量管理
│       ```pine
│       // 批量管理绘图对象
│       var line[] lines = array.new<line>()
│       // 添加、更新、删除逻辑
│       ```
│
└─ 📊 应用场景
    ├─ 支撑阻力位
    │   ```pine
    │   // 绘制支撑阻力
    │   hline(support, "支撑", color.green)
    │   hline(resistance, "阻力", color.red)
    │   fill(support, resistance, color=color.gray)
    │   ```
    │
    ├─ 通道
    │   ```pine
    │   // 价格通道
    │   upper = ma + 2 * ta.stdev(close, 20)
    │   lower = ma - 2 * ta.stdev(close, 20)
    │   p1 = plot(upper)
    │   p2 = plot(lower)
    │   fill(p1, p2, color=color.new(color.blue, 90))
    │   ```
    │
    └─ 时间窗口
        ```pine
        // 标记时间范围
        box.new(startBar, topPrice, endBar, bottomPrice,
                bgcolor=color.new(color.yellow, 90))
        ```
```

## 📋 Tables/Backgrounds（结构化数据）

```
┌─ 选择：Tables/Backgrounds
│
├─ 📊 信息面板类型？
│   │
│   ├─ 简单信息显示
│   │   └─ ✅ **文本标签组合**
│   │       ```pine
│   │       // 使用标签创建信息面板
│   │       var label infoPanel = na
│   │       if na(infoPanel)
│   │       infoPanel := label.new(
│   │           x=bar_index, y=highest,
│   │           text="RSI: " + str.tostring(rsi),
│   │           style=label.style_label_down,
│   │           size=size.normal)
│   │       else
│   │       label.set_text(infoPanel, updateText)
│   │       ```
│   │
│   ├─ 表格数据
│   │   └─ ✅ **table.new()**
│   │       ```pine
│   │       // 创建表格
│   │       var table infoTable = table.new(position.top_right, 2, 4,
│   │           bgcolor=color.white,
│   │           border_width=1)
│   │
│   │       // 设置表格内容
│   │       if barstate.islast
│   │           table.cell(infoTable, 0, 0, "指标", bgcolor=color.gray)
│   │           table.cell(infoTable, 1, 0, "值", bgcolor=color.gray)
│   │           table.cell(infoTable, 0, 1, "RSI")
│   │           table.cell(infoTable, 1, 1, str.tostring(rsi, "#.##"))
│   │           table.cell(infoTable, 0, 2, "MACD")
│   │           table.cell(infoTable, 1, 2, str.tostring(macd, "#.####"))
│   │       ```
│   │
│   └─ 背景高亮
│       └─ ✅ **bgcolor()**
│           ```pine
│           // 背景条件着色
│           bgColor = rsi > 70 ? color.new(color.red, 90) :
│                      rsi < 30 ? color.new(color.green, 90) :
│                      na
│           bgcolor(bgColor)
│           ```
│
├─ 🎨 表格样式
│   │
│   ├─ 位置设置
│   │   ```pine
│   │   position.top_left      // 左上
│   │   position.top_center    // 上中
│   │   position.top_right     // 右上
│   │   position.middle_left   // 左中
│   │   position.middle_center // 正中
│   │   position.middle_right  // 右中
│   │   position.bottom_left   // 左下
│   │   position.bottom_center // 下中
│   │   position.bottom_right  // 右下
│   │   ```
│   │
│   ├─ 单元格样式
│   │   ```pine
│   │   table.cell(table_id, col, row, text,
│   │       bgcolor=color.blue,        // 背景色
│   │       text_color=color.white,    // 文字色
│   │       text_size=size.normal,     // 文字大小
│   │       text_halign=text.align_left,   // 水平对齐
│   │       text_valign=text.align_top)    // 垂直对齐
│   │   ```
│   │
│   └─ 边框设置
│       ```pine
│       table.new(...,
│           border_width=1,          // 边框宽度
│           border_color=color.gray) // 边框颜色
│       ```
│
├─ 💡 最佳实践
│   │
│   ├─ 更新策略
│   │   ```pine
│   │   // 仅在最后一根K线更新
│   │   if barstate.islast
│   │       updateTable()
│   │   ```
│   │
│   ├─ 性能优化
│   │   ```pine
│   │   // 避免每根K线都创建表格
│   │   var table myTable = na
│   │   if na(myTable)
│   │       myTable := table.new(...)
│   │   ```
│   │
│   └─ 响应式设计
│       ```pine
│       // 根据屏幕大小调整
│       tableSize = syminfo.isbinary ? 2 : 4
│       ```
│
└─ 📋 高级功能
    ├─ 合并单元格
    │   ```pine
    │   // Pine Script v6 支持单元格合并
    │   table.merge_cells(table, 0, 0, 1, 0)
    │   ```
    │
    ├─ 渐变背景
    │   ```pine
    │   // 创建渐变效果
    │   for i = 0 to 10
    │       alpha = i * 10
    │       bgcolor(color.new(color.blue, alpha))
    │   ```
    │
    └─ 动态内容
        ```pine
        // 根据条件显示不同内容
        table.cell(table, 0, 0,
            marketStatus ? "市场开放" : "市场关闭",
            marketStatus ? color.green : color.red)
        ```
```

## 🎨 混合方案

```
┌─ 选择：混合多种可视化方式
│
├─ 📊 复合图表示例
│   └─ ✅ **完整技术分析界面**
│       ```pine
│       // 1. 背景
│       bgcolor(ma20 > ma50 ? color.new(color.green, 95) :
│                          color.new(color.red, 95))
│
│       // 2. 主图 - 价格和移动平均
│       plot(close, "收盘价", color.black)
│       plot(ma20, "MA20", color.blue)
│       plot(ma50, "MA50", color.red)
│
│       // 3. 信号标记
│       plotshape(buySignal, "买入", shape.triangleup,
│                  location.belowbar, color.green, size=size.small)
│       plotshape(sellSignal, "卖出", shape.triangledown,
│                  location.abovebar, color.red, size=size.small)
│
│       // 4. 支撑阻力
│       hline(support, "支撑", color.green, linestyle=hline.style_dashed)
│       hline(resistance, "阻力", color.red, linestyle=hline.style_dashed)
│
│       // 5. 信息面板
│       if barstate.islast
│           createInfoPanel()
│       ```
│
├─ 🎯 选择原则
│   │
│   ├─ 不要过度装饰
│   │   ❌ 太多颜色、标记、线条
│   │   ✅ 保持简洁清晰
│   │
│   ├─ 信息层次清晰
│   │   - 主要数据：最醒目
│   │   - 次要数据：较淡
│   │   - 参考信息：最小化
│   │
│   ├─ 颜色使用规范
│   │   - 绿色：看涨/积极
│   │   - 红色：看跌/消极
│   │   - 蓝色：中性信息
│   │   - 黄色/橙色：警告
│   │
│   └─ 性能考虑
│       - 限制绘图对象数量
│       - 合理更新频率
│       - 避免重复绘制
│
└─ 📝 调试技巧
    ├─ 使用 display 参数控制显示
    │   ```pine
    │   plot(debugValue, display=display.none)  // 仅数据窗口显示
    │   ```
    │
    ├─ 条件显示调试信息
    │   ```pine
    │   if debugMode
    │       label.new(bar_index, high, "Debug: " + str.tostring(value))
    │   ```
    │
    └─ 使用不同颜色区分版本
        ```pine
        v1Color = version == 1 ? color.blue : color.gray
        plot(value1, color=v1Color)
        ```
```

## 📊 可视化决策清单

### Plot 选择清单
- [ ] 数据是否连续？
- [ ] 需要显示趋势吗？
- [ ] 需要填充区域吗？
- [ ] 需要特殊样式吗？

### Shape/Label 选择清单
- [ ] 事件是否离散？
- [ ] 需要显示详细信息吗？
- [ ] 标记位置是否重要？
- [ ] 需要限制数量吗？

### Line/Box 选择清单
- [ ] 需要连接多个点吗？
- [ ] 需要显示区域吗？
- [ ] 需要延伸线条吗？
- [ ] 需要动态更新吗？

### Table 选择清单
- [ ] 需要显示结构化数据吗？
- [ ] 需要多行多列吗？
- [ ] 需要实时更新吗？
- [ ] 需要特殊样式吗？

## ⚠️ 常见错误避免

1. **过度绘图**：太多元素导致混乱
2. **颜色冲突**：相似颜色难以区分
3. **性能问题**：过多动态对象
4. **信息过载**：显示太多信息
5. **位置重叠**：元素相互遮挡
6. **更新频繁**：每个tick都更新

记住：**好的可视化是清晰传达信息，而不是展示所有可能**。选择最简单有效的方式来表达你的数据。