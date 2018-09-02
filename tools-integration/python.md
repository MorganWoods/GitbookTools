---
description: 与编程相关的知识记录
---

# Python

## 常用函数

* `assert`

  断言, 其后面的判断为假时候就出现错误.是编程序时候用的检查程序的作用.后面为真,则什么都不做.

* `hasattr()` 用于确定一个对象中是否具有某个属性,返回一个布尔值   `hasattr(object,name)`  
* `idxmax()` 返回最大值的索引
* `flatten`

  处理矩阵或数组,把其降到一维,默认横着方向降维原数据,若按竖着方向处理源数据, `flatten('F')`

* `zip()`

  将可迭代的对象作为参数,将对象中对应的元素打包成一个个元组,然后返回由元组组成的列表.

  ​

## 一些库

* `shutil` :高层次文件操作工具

### Numpy

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
•
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

### 有关 matplotlib 画图

* 绘制多个独立窗口图表为不同窗口图标起不同名字,为里添加内容.并在程序最终统一显示,即刻绘制多个独立窗口表格

```text
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
# 程序最后显示窗口
plt.show()
```

* 保存图表  

```text
plt.plot()
plt.savefig('PATH and name.jpg')
plt.show
```

## 数学知识记录

* 方差 variance; 标准差 standard deviation; 均方误差 MSE\(mean squared error\); 均方根值 RMS;

  **方差**衡量离散程度 ; **标准差**又称为 **均方差**, 是方差的算术平方根,反映数据集的离散程度. 与方差类似, 只是方差有平方项,不如标准差直观.**均方误差**衡量 平均误差 ,是参数估计值与参数真值之差的平方的期望值.常用在信号处理的滤波算法中.表示此时观测值与估计值之间的偏差.**均方根值**也称为方均根值或有效值,先平方,再平均,然后开放.**均方根误差**是均方误差的算术平方根.

### 双端队列

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

