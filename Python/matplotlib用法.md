## Matplotlib用法

### plot

线型图，示例代码如下：

```python
from matplotlib import pyplot as plt

days = [0, 1, 2, 3, 4, 5, 6]
money_spent = [10, 12, 12, 10, 14, 22, 24]
# 第一个参数是横坐标，第二个参数是纵坐标
plt.plot(days, money_spent)
plt.show()
```

`pyplot.plot()`,函数接收横坐标、纵坐标两个参数数组两个参数。调用`pyplot.show()`可以显示当前线型图。

有时候我们想对比同一横坐标下，两组数据的对比。此时可以调用两次`pyplot.plot()`函数，该库会默认给出两条颜色不同的线型图来展示数据，大致代码如下：

```python
from matplotlib import pyplot as plt
# 时间
time = [0, 1, 2, 3, 4]
# 收入
revenue = [200, 400, 650, 800, 850]
# 支出
costs = [150, 500, 550, 550, 560]
# 时间-支出，时间-收入两条线型图
plt.plot(time, revenue)
plt.plot(time, costs)
# 只需要调用一次show方法
plt.show()
```

有些时候我们想要自己设置线条的颜色以及其他内容，此时可以传入`color`以及`linestyle`等参数，详细信息见 [Matplotlib documentation](https://matplotlib.org/api/lines_api.html)文档。示例代码如下：

```python
from matplotlib import pyplot as plt

time = [0, 1, 2, 3, 4]
revenue = [200, 400, 650, 800, 850]
costs = [150, 500, 550, 550, 560]
# 收入-时间线型图，线条颜色：紫，线条类型：虚线；支出-时间线型图，颜色：#82edc9，点类型：方形
plt.plot(revenue, time, color='purple', linestyle='--')
plt.plot(costs, time, color='#82edc9', marker='s')
plt.show()
```

调用`pyplot.axis([x_from, x_to, y_from, y_to])`可以手动定义坐标轴的范围。示例代码如下：

```python
from matplotlib import pyplot as plt

x = range(12)
y = [3000, 3005, 3010, 2900, 2950, 3050, 3000, 3100, 2980, 2980, 2920, 3010]
plt.plot(x, y)
# 设置x轴从0到12，y轴从2900到3100
plt.axis([0, 12, 2900, 3100])
plt.show()
```

一般图型都有对坐标轴的描述，这里也可以设置。通过调用`pyplot.xlabel(str)`以及`pyplot.xlabel(str)`能分别设置x轴，y轴描述;通过`pyplot.title(str)`函数可以设置图的标题。示例代码如下：

```python
from matplotlib import pyplot as plt

x = range(12)
y = [3000, 3005, 3010, 2900, 2950, 3050, 3000, 3100, 2980, 2980, 2920, 3010]
plt.plot(x, y)
plt.axis([0, 12, 2900, 3100])
plt.xlabel('Time')
plt.ylabel('Dollars spent on coffee')
plt.title('My Last Twelve Years of Coffee Drinking')
plt.show()
```

**matplotlib**还支持在一张图中同时输出多张子图，使用`pyplot.subplot(rows, columns, index)`来定义有多少个子图以及目前处理第多少个子图，注意，这里`index`下标从*1*开始计数。示例代码如下：

```python
from matplotlib import pyplot as plt

months = range(12)
temperature = [36, 36, 39, 52, 61, 72, 77, 75, 68, 57, 48, 48]
flights_to_hawaii = [1200, 1300, 1100, 1450, 850, 750, 400, 450, 400, 860, 990, 1000]
# 设置为一行两列子图，当前处理第一个子图
plt.subplot(1, 2, 1)
plt.plot(temperature, months)
# 当前处理第二个子图
plt.subplot(1, 2, 2)
plt.plot(flights_to_hawaii,temperature,marker='o')
plt.show()
```

有时候，也有打印三个子图，第一行打印一个子图，第二行打印两个子图这类情况以及子图间的间距。这种情况下，要尤其注意子图的`index`。示例代码如下:

```python
from matplotlib import pyplot as plt

x = range(7)
straight_line = [0, 1, 2, 3, 4, 5, 6]
parabola = [0, 1, 4, 9, 16, 25, 36]
cubic = [0, 1, 8, 27, 64, 125, 216]
# 选择第一行的子图，index为1
plt.subplot(2, 1, 1)
plt.plot(straight_line, x)
# 选择第二行的第一个子图，index为3
plt.subplot(2, 2, 3)
plt.plot(x, parabola)
# 选择第二行的第二个子图，index为4
plt.subplot(2, 2, 4)
plt.plot(x, cubic)
# 设置图形间横空格，以及低间距
plt.subplots_adjust(wspace=0.35, bottom=0.2)
plt.show()
```

设置图例，就是图形旁边标记的线段标题：

```python
from matplotlib import pyplot as plt

months = range(12)
hyrule = [63, 65, 68, 70, 72, 72, 73, 74, 71, 70, 68, 64]
kakariko = [52, 52, 53, 68, 73, 74, 74, 76, 71, 62, 58, 54]
gerudo = [98, 99, 99, 100, 99, 100, 98, 101, 101, 97, 98, 99]

plt.plot(months, hyrule)
plt.plot(months, kakariko)
plt.plot(months, gerudo)

legend_labels = ["Hyrule", "Kakariko", "Gerudo Valley"]
plt.legend(legend_labels, loc=9)

plt.show()
```

更改坐标轴的描述，比如x轴数字月份改为文字月份，示例代码如下：

```python
from matplotlib import pyplot as plt

month_names = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep","Oct", "Nov", "Dec"]

months = range(12)
conversion = [0.05, 0.08, 0.18, 0.28, 0.4, 0.66, 0.74, 0.78, 0.8, 0.81, 0.85, 0.85]

plt.xlabel("Months")
plt.ylabel("Conversion")
ax = plt.subplot(1, 1, 1)
plt.plot(months, conversion)

# 设置x坐标轴坐标为月份描述
ax.set_xticks(months)
ax.set_xticklabels(month_names)
# 设置y坐标轴坐标为百分比坐标
ax.set_yticks([0.10, 0.25, 0.5, 0.75])
ax.set_yticklabels(['10%', '25%', '50%', '75%'])
plt.show()
```

如下是新建*figure*、关闭之前的图形*close*、保存图片的简单示例：

```python
from matplotlib import pyplot as plt

word_length = [8, 11, 12, 11, 13, 12, 9, 9, 7, 9]
power_generated = [753.9, 768.8, 780.1, 763.7, 788.5, 782, 787.2, 806.4, 806.2, 798.9]
years = [2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009]

plt.close('all')
plt.figure()
plt.plot(years, word_length)
plt.savefig('winning_word_lengths.png')

plt.figure(figsize=(7,3))
plt.plot(years, power_generated)
plt.savefig('power_generated.png')
plt.show()
```



**legend的loc参数对应数字表**

| Number Code | String       |
| ----------- | ------------ |
| 0           | best         |
| 1           | upper right  |
| 2           | upper left   |
| 3           | lower left   |
| 4           | lower right  |
| 5           | right        |
| 6           | center left  |
| 7           | center right |
| 8           | lower center |
| 9           | upper center |
| 10          | center       |

### bar

**最基础的柱状图**
`pyplot.bar()`柱状图。同样接受两个*float*类型的数组作为`x`轴，`y`轴。示例如下：

```python
from matplotlib import pyplot as plt
# 饮品与销售量柱状图
drinks = ["cappuccino", "latte", "chai", "americano", "mocha", "espresso"]
sales =  [91, 76, 56, 66, 52, 27]
# x轴暂时展示序号
plt.bar(range(len(drinks)), sales)
plt.show()
```

柱状图同样也可以使用`ax = plt.subplot()`获取坐标轴，后续同样使用`set_xticks`、`set_xticklabels`等方法设置坐标轴的名称。示例代码如下：
```python
from matplotlib import pyplot as plt

drinks = ["cappuccino", "latte", "chai", "americano", "mocha", "espresso"]
sales =  [91, 76, 56, 66, 52, 27]
ax = plt.subplot()
ax.set_xticks(range(len(drinks)))
ax.set_xticklabels(drinks)
plt.bar(range(len(drinks)), sales)
plt.show()
```
**并列对比的柱状图**
同一柱状图中也能有多个数据集来对比不同，此时与线型图不同的位置是，两个对比的数据集取的X轴不能相同，否则柱状图就会相互重叠，相互覆盖。示例如下：
```python
from matplotlib import pyplot as plt

drinks = ["cappuccino", "latte", "chai", "americano", "mocha", "espresso"]
sales1 =  [91, 76, 56, 66, 52, 27]
sales2 = [65, 82, 36, 68, 38, 40]

#Paste the x_values code here
n = 1  # This is our first dataset (out of 2)
t = 2 # Number of datasets
d = 6 # Number of sets of bars
w = 2/3 # Width of each bar
x_values1 = [t*element + w*n for element in range(d)]
store1_x = x_values1

n = 2 # This is our first dataset (out of 2)
t = 2 # Number of datasets
d = 6 # Number of sets of bars
w = 2/3 # Width of each bar
x_values2 = [t*element + w*n for element in range(d)]
store2_x = x_values2

plt.bar(store1_x, sales1)
plt.bar(store2_x, sales2)
plt.show()
```

**堆叠柱状图**

一个图在另一个图上面堆叠，示例如下：

```python
from matplotlib import pyplot as plt

drinks = ["cappuccino", "latte", "chai", "americano", "mocha", "espresso"]
sales1 =  [91, 76, 56, 66, 52, 27]
sales2 = [65, 82, 36, 68, 38, 40]

ax_x = range(len(drinks))

plt.bar(ax_x, sales1)
plt.bar(ax_x, sales2, bottom=sales1)
plt.legend(["Location 1", "Location 2"])
plt.show()

```

**误差图**

柱状图数据有时候会有一些误差，此时可以使用指定参数`yerr`来指定误差范围，指定`yerr`为一个数字时，则每个柱误差都是这个数。指定为一个`list`时，每一个柱对应一个误差。设置`capsize`参数可以让误差看得更明显。

```python
from matplotlib import pyplot as plt

drinks = ["cappuccino", "latte", "chai", "americano", "mocha", "espresso"]
ounces_of_milk = [6, 9, 4, 0, 9, 0]
error = [0.6, 0.9, 0.4, 0, 0.9, 0]

# Plot the bar graph here
plt.bar(range(len(drinks)), ounces_of_milk, yerr=error, capsize=10)
plt.show()
```

