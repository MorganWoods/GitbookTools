---
description: relate to Coding within python
---

# Python

## General 

```text
#check python bit
import platform   
platform.architecture()
```

## Functions

* `assert`

  断言, 其后面的判断为假时候就出现错误.是编程序时候用的检查程序的作用.后面为真,则什么都不做.

* `hasattr()` 用于确定一个对象中是否具有某个属性,返回一个布尔值   `hasattr(object,name)`  
* `idxmax()` 返回最大值的索引
* `flatten`

  处理矩阵或数组,把其降到一维,默认横着方向降维原数据,若按竖着方向处理源数据, `flatten('F')`

* `zip()`

  将可迭代的对象作为参数,将对象中对应的元素打包成一个个元组,然后返回由元组组成的列表.

  ​

## Library 🌀

* `shutil` :高层次文件操作工具

### ➡ Numpy

* `np.newaxis` :增加一个维度.
* `np.random.permutation(state_action.imdex)` 洗牌功能,打乱次序. index 与 columns 对应, index 是 row 的标签
* `np.random.choice(a, size=None, replace=True, p=None)`

  从 a 中随机算去size 个量,结果放入 array 中返回. p 是可以设置出现概率.

* `np.clip(a, a_min, a_max, out=None)`

  把a 中小于 a\_min 的值用 a\_min 代替,把大于 a\_max 的值用a\_max 代替.

* 使用双端队列的形式求数据的方差,标准差,均值等

  ```text
  import numpy as np
  from collections import deque   #使用双端队列
  ​
  d =deque(maxlen=5) #设置队列最大容量
  L =len(d) #用来计队列的长度.
  fori inrange(10):
    d.append(i)
    i+=1
  print('d=',d)
  var =np.var(d) #计算方差
  print('var=',var)
  mean =np.mean(d)  #均值
  print('mean=',mean)
  np.std(d) # 标准差
  ```

```text
​
## 零散知识
* python 中小括号代表元组;中括号代表列表;大括号代表字典.
* 引用同级文件夹下的 py 文档
```python
import sys 
sys.path.append("..")
from <文件夹>.<py文件> import <模块>
```

* 有关下划线
  * 单下划线   用在循环中计数中,但是对它的值并不关心,而且在下文不会调用此值时,习惯用\_
  * 名称前的下划线\(如: \_shahriar\)  指定该名称属性为私有,仅供内部使用.视为 API 中非公开部分,在修改他们时无需对外部通知.  
  * 名称前的双下划线\(\_\_shahriar\)  这种用法不是惯例,对解释器来说有特定含义,避免与子类定义的名称冲突.不太懂
  * 名称前后的双下划线\(\_\_init\_\_\)  这种用法表示 Python 中特殊的方法名.是一种惯例.这将确保不会与用户自定义的名称冲突.  
* python3 与 2 区别  python3中使用 print\(""\)  python2中    print ""
* python 中的 None   &lt;br&gt;它既不是0，也不是False，也不是空字符串。它只是一个空值的对象，也就是一个空的对象，只是没有赋值而已。
* 哈希?

  哈希表是一种能实现关联数组的抽象数据结构，能把很多「键」映射到很多「值」上。哈希表使用哈希函数来计算索引，一个索引对应一个值。

* 类 class

  类是抽象模板,类名的括号里表示从哪个类继承下来的.\_\_init\_\_方法第一个参数永远是 self;

  如果让内部属性不被外部访问,就可以把属性的名称前加两个下划线,就成为了私有变量.只有内部可以访问.

  前后都有两个下划线的变量名是特殊变量;以单个下划线开头的变量是外部可以访问的.他的实际含义是:虽然我可以被访问,但是请把我视为私有变量,不要随意访问.

  类中定义的功能称之为方法.

* 类中函数的互相调用小结

  在勒种的定义实例方法时要加一个 self 参数.

### ➡ Matplotlib

![](../.gitbook/assets/image%20%282%29.png)

* plot muti-figures , display them before ending.

```python
# figure1
plt.figure('figure1')
plt.plot(np.arange(len(self.qtarget_his)),self.qtarget_his,c='r',label='DQN Q eval')
plt.legend(loc='best') #设置图例,自动分配
plt.ylabel('Q_target value')
plt.xlabel('training steps')
# figure2
plt.figure('cost')
plt.plot(np.arange(len(self.cost_his)), self.cost_his)
plt.legend(loc='best')
plt.ylabel('Cost')
plt.xlabel('training steps')
# display
plt.show()
```

* save figures

```text
plt.plot()
plt.savefig('PATH and name.jpg')
plt.show

```

#### ➡➡ Samples

> next parts from: [https://www.datascience.com/learn-data-science/tutorials/creating-data-visualizations-matplotlib-data-science-python](https://www.datascience.com/learn-data-science/tutorials/creating-data-visualizations-matplotlib-data-science-python)

* scatter plot

```python
# Define a function to create the scatterplot. This makes it easy to
# reuse code within and across notebooks
def scatterplot(x_data, y_data, x_label, y_label, title):

    # Create the plot object
    _, ax = plt.subplots()

    # Plot the data, set the size (s), color and transparency (alpha)
    # of the points
    ax.scatter(x_data, y_data, s = 30, color = '#539caf', alpha = 0.75)

    # Label the axes and provide a title
    ax.set_title(title)
    ax.set_xlabel(x_label)
    ax.set_ylabel(y_label)

# Call the function to create plot
scatterplot(x_data = daily_data['temp']
            , y_data = daily_data['cnt']
            , x_label = 'Normalized temperature (C)'
            , y_label = 'Check outs'
            , title = 'Number of Check Outs vs Temperature')
```

* line plot

```python
# Perform linear regression
import statsmodels.api as sm
from statsmodels.stats.outliers_influence import summary_table
x = sm.add_constant(daily_data['temp'])
y = daily_data['cnt']
regr = sm.OLS(y, x)
res = regr.fit()
# Get fitted values from model to plot
st, data, ss2 = summary_table(res, alpha=0.05)
fitted_values = data[:,2]

# Define a function for the line plot
def lineplot(x_data, y_data, x_label, y_label, title):
    # Create the plot object
    _, ax = plt.subplots()

    # Plot the best fit line, set the linewidth (lw), color and
    # transparency (alpha) of the line
    ax.plot(x_data, y_data, lw = 2, color = '#539caf', alpha = 1)

    # Label the axes and provide a title
    ax.set_title(title)
    ax.set_xlabel(x_label)
    ax.set_ylabel(y_label)

# Call the function to create plot
lineplot(x_data = daily_data['temp']
         , y_data = fitted_values
         , x_label = 'Normalized temperature (C)'
         , y_label = 'Check outs'
         , title = 'Line of Best Fit for Number of Check Outs vs Temperature')
```

* line plot with **confidence intervals**

  We can take this analysis one step further and also visualize the 95% confidence intervals about our model. This will help communicate how well our model fits the data.  
  confidence intervals: Confidence intervals are constructed at a confidence level, such as 95 %, selected by the user. What does this mean? It means that if the same population is sampled on numerous occasions and interval estimates are made on each occasion, the resulting intervals would bracket the true population parameter in approximately 95 % of the cases. A confidence stated at a 1−αlevel can be thought of as the inverse of a significance level, α.

```python
# Get the confidence intervals of the model
predict_mean_ci_low, predict_mean_ci_upp = data[:,4:6].T

# Data for regions where we want to shade to indicate the intervals has
# to be sorted by the x axis to display correctly
CI_df = pd.DataFrame(columns = ['x_data', 'low_CI', 'upper_CI'])
CI_df['x_data'] = daily_data['temp']
CI_df['low_CI'] = predict_mean_ci_low
CI_df['upper_CI'] = predict_mean_ci_upp
CI_df.sort_values('x_data', inplace = True)

# Define a function for the line plot with intervals
def lineplotCI(x_data, y_data, sorted_x, low_CI, upper_CI, x_label, y_label, title):
    # Create the plot object
    _, ax = plt.subplots()

    # Plot the data, set the linewidth, color and transparency of the
    # line, provide a label for the legend
    ax.plot(x_data, y_data, lw = 1, color = '#539caf', alpha = 1, label = 'Fit')
    # Shade the confidence interval
    ax.fill_between(sorted_x, low_CI, upper_CI, color = '#539caf', alpha = 0.4, label = '95% CI')
    # Label the axes and provide a title
    ax.set_title(title)
    ax.set_xlabel(x_label)
    ax.set_ylabel(y_label)

    # Display legend
    ax.legend(loc = 'best')

# Call the function to create plot
lineplotCI(x_data = daily_data['temp']
           , y_data = fitted_values
           , sorted_x = CI_df['x_data']
           , low_CI = CI_df['low_CI']
           , upper_CI = CI_df['upper_CI']
           , x_label = 'Normalized temperature (C)'
           , y_label = 'Check outs'
           , title = 'Line of Best Fit for Number of Check Outs vs Temperature')
```

* histogram Histograms are used to get a rough idea of how a quantitative variable is distributed. The observed values are placed into different bins and the frequency of observations in each of those bins is calculated. For this example, let's examine the distribution of registered bike checkouts.

```python
# Define a function for a histogram
def histogram(data, x_label, y_label, title):
    _, ax = plt.subplots()
    ax.hist(data, color = '#539caf')
    ax.set_ylabel(y_label)
    ax.set_xlabel(x_label)
    ax.set_title(title)

# Call the function to create plot
histogram(data = daily_data['registered']
           , x_label = 'Check outs'
           , y_label = 'Frequency'
           , title = 'Distribution of Registered Check Outs')
```

* Box plot

  Box plots are most suited to displaying the distribution of a variable across multiple groups. The bottom and top of the boxes indicate the lower and upper quartiles, respectively, and the line inside the box is for the median. Vertical lines extending from the boxes \("whiskers"\) show the range of the data \(by default, this is 1.5x past the upper and lower quartiles in matplotlib\). Box plots can be thought of as a hybrid between bar plots and overlaid histograms. They surface much of the same information as bar plots, but they also expose the variation in the data. However, they do not show the underlying distribution of the data.

```python
# Unlike with bar plots, there is no need to aggregate the data
# before plotting
# However the data for each group (day) needs to be defined
days = np.unique(daily_data['weekday'])
bp_data = []
for day in days:
    bp_data.append(daily_data[daily_data['weekday'] == day]['cnt'].values)

# Define a function to create a boxplot:
def boxplot(x_data, y_data, base_color, median_color, x_label, y_label, title):
    _, ax = plt.subplots()

    # Draw boxplots, specifying desired style
    ax.boxplot(y_data
               # patch_artist must be True to control box fill
               , patch_artist = True
               # Properties of median line
               , medianprops = {'color': median_color}
               # Properties of box
               , boxprops = {'color': base_color, 'facecolor': base_color}
               # Properties of whiskers
               , whiskerprops = {'color': base_color}
               # Properties of whisker caps
               , capprops = {'color': base_color})

    # By default, the tick label starts at 1 and increments by 1 for
    # each box drawn. This sets the labels to the ones we want
    ax.set_xticklabels(x_data)
    ax.set_ylabel(y_label)
    ax.set_xlabel(x_label)
    ax.set_title(title)

# Call the function to create plot
boxplot(x_data = days
        , y_data = bp_data
        , base_color = '#539caf'
        , median_color = '#297083'
        , x_label = 'Day of week'
        , y_label = 'Check outs'
        , title = 'Total Check Outs By Day of Week (0 = Sunday)')
```

#### ➡➡How to plot bold value with shade area deviation?

Calculate mean and std. fill between \(mean-std, mean+std\).

```python
plt.style.use('ggplot') #Change/Remove This If you Want ⭐️

fig, ax = plt.subplots(figsize=(8, 4))
#ax.plot(trees_grid, train_acc.mean(axis=1), alpha=0.5, color='blue', label='train', linewidth = 4.0)
ax.plot(trees_grid, test_acc.mean(axis=1), alpha=0.5, color='red', label='cv', linewidth = 1.0)
ax.fill_between(trees_grid, test_acc.mean(axis=1) \
    - test_acc.std(axis=1), test_acc.mean(axis=1) + \
    test_acc.std(axis=1), color='#888888', alpha=0.4)
ax.fill_between(trees_grid, test_acc.mean(axis=1) \
    - 2*test_acc.std(axis=1), test_acc.mean(axis=1) \
    + 2*test_acc.std(axis=1), color='#888888', alpha=0.2)
ax.legend(loc='best')
ax.set_ylim([0.88,1.02]) # ⭐️
ax.set_ylabel("Accuracy")
ax.set_xlabel("N_estimators")
```

### ➡ Pandas

| Object Type | Selection | Return Value Type |
| :--- | :--- | :--- |
| Series | `series[label]` | scalar value |
| DataFrame | `frame[colname]` | `Series` corresponding to colname |
| Panel | `panel[itemname]` | `DataFrame` corresponding to the itemname |

```python
pd.Series([...]) # basic form
df = pd.DataFrame() #dataframe 
df.head() ;  df.tail(3) #viewing data

# rolling means etc.
```

## Mathematics knowledge 🌀

*  variance;  standard deviation;  MSE\(mean squared error\);  RMS;

  \*\*\*\*

* standard deviation \(SD\) formula: $$sd=\sqrt{\sum{|x-\mu|^{2} }/N} $$  where x is a value in the data set, /mu is the mean of the data set, and N is the number of data points in the population.

### Dequeue

double ended queue

```text
from collections import deque  #头文件：
常用的方法：
d =deque([])  # 创建一个空的双队列
d.append(item)   # 在d的右边(末尾)添加项目item
d.appendleft(item)  # 从d的左边(开始)添加项目item
d.clear()  # 清空队列，也就是删除d中的所有项目
d.extend(iterator)   # 在d的右边(末尾)添加iterator中的所有项目
d.extendleft(item)  # 在d的左边(开始)添加item中的所有项目
d.pop()   # 删除并返回d中的最后一个(最右边的)项目。如果d为空，则引发IndexError
d.popleft()   # 删除并返回d中的第一个(最左边的)项目。如果d为空，则引发IndexError
d.count(n)  # 在队列中统计元素的分数，n表示统计的元素
d.remove(n)  # 从队列中删除指定的值
d.reverse()  # 翻转队列
d.rotate(n=1)  # 将d向右旋转n步(如果n<0，则向左旋转)
#判断队列d是否为空
ifd:   # 或者用 len(d) 判断.
    # 如果不为空时
else:
  # 如果为空时
#取出d的左边和右边元素：
#d[0]：取出最左边元素
#d[-1]：取出最右边元素
```



