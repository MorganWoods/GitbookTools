# TensorFlow



### 基础知识

* 官方教程笔记

  > [TF中文教程](file:///Users/menghaw1/Downloads/0_wmh/7_Project3Pygame/NoteBook/Tensorflow.md#)

  Tensorflow不单独地运行单一的复杂计算，而是让我们可以先用图描述一系列可交互的计算操作，然后全部一起在Python之外\(就是 feed 的数值\)运行。（这样类似的运行方式，可以在不少的机器学习库中看到。）

  `x = tf.placeholder(tf.float32, [None, 784])` : x 是一个占位符,此张量的 shape 是\[None,784\] None 表示第一个维度可以是任何长度. 一般用来为输入值占位置.

  一个`Variable`代表一个可修改的张量,可以用来计算输入值,也可以在计算中被修改,一般存放模型参数`W = tf.Variable(tf.zeros([784,10]))` `b = tf.Variable(tf.zeros([10]))` ;用`tf.matmul(X，W)`表示`x`乘以`W`对应公式中的 Wx , 因为他们的 shape 原因.\[None,784\]x\[784,10\]+\[10\];一旦被定义好之后，我们的模型就可以在不同的设备上运行：计算机的CPU，GPU，甚至是手机！

  在训练模型的时候一般要最小化 cost 或 loss, 还有个非常不错的成本函数是交叉熵.

  tf 自动使用反向传播算法来有效的确定变量是如何影响你要最小化的那个成本值得,`train_step = tf.train.GradientDescentOptimizer(0.01).minimize(cross_entropy)`, 以0.01的速率最小化交叉熵

  创建网络常用操作如下:

  ```python
  hidden1 =tf.nn.relu(tf.matmul(images, weights) +biases)
  hidden2 =tf.nn.relu(tf.matmul(hidden1, weights) +biases)
  logits =tf.matmul(hidden2, weights) +biases
  ```

  `loss = tf.reduce_mean(cross_entropy, name='xentropy_mean')`

  `tf.scalar_summary(loss.op.name, loss)#记录图表`

  教程中 CIFAR-10教程中有一种机制可以实现学习率随着时间的推移而递减.⭐️

  ​

* 莫烦教程笔记

  tensorflow: 飞行的数据. 在输入层输入数据,其飞到隐藏层与输出层,用梯度下降对参数进行更新,然后循环到收敛;

  tf.Variable 定义变量,与 python 不同, tf 必须先定义它是变量,才能使用.

  要给节点输入数据时使用 placehoder, 其与 feed\_dict 是绑定使用的.

  dropout 在 tf 中的一个工具,给他赋予不被 drop 的百分比,可以降低过拟合.

  训练好的神经网络目前 tf 只能保存 variables, 不能保存整个网络的的框架.再次使用时候需要重新定义框架,然后把 variables 放进去学习.

* 基本属性
  * Graph

    使用**图\(graph\)** 来表示计算任务.有边与点;圆圈代表常量\(const\);椭圆代表操作\( Op\) ;圆角方框代表子图;边代表张量的流向,边上的标记代表张量的形状,\(其中,若张量1阶,标记为 scalar, 高阶的标记为 m\*n\)

  * 在被称之为**会话\(Session\)** 的**上下文\(context\)** 中执行图.&lt;br&gt;

    Session: 用于执行图.每次 sess.run 的时候才进行真正的计算

  * 使用 **tensor** 表示数据.

    零阶张量为scalar 如\[1\], 一阶张量 vector如\[1,2,3,\],二阶张量 matrix,

  * Variable

    通过 **变量 \(Variable\)** 维护状态.

    表达,更新,存储模型参数.其可变更, 初始化时被添加默认的 collection 中.

    在整个 session 运行前, Graph 中所有 variable 必须被初始化

    ```text
    sess =tf.Session()
    init =tf.initialize_all_variables() 
    sess.run(init)
    ```

    tensorflow 中定义某个字符串为变量后它才是变量,与 python 不同.

  * Tensor: 类型化的多维数组,图的边.
  * Operation

    执行计算的单元,节点node. 在 run 之后才会执行.

  * 使用 feed 和 fetch 可以为任意的操作\(arbitrary operation\) 赋值或者从其中获取数据.

    feed一般使用字典形式临时替换值,在该方法结束后自动失效.&lt;br&gt;

  * Collection

    用来组织不同类别的对象,提供一种零存整取思路,全局存储机制,在每个层次可以创造对象,存入相应 collection 中;创造完成后可以统一从一个 collection 中取出一类变量,进而施加操作.

    在 tf.GraphKeys 中包含了所有默认 collections 的名称. Variable 被收集在名为 tf.GraphKeys.VARIABLES中.

    ```text
    tf.Graph.add_to_collection(name, value)#向名字为 name 的 collection中存数据
    tf.add_to_collection(name, value)#这个和上面函数功能上没有区别，区别是，这个函数是给默认图使用的
    tf.Graph.get_collection(name, scope=None)#获取数据
    ```

    tf自己也维护一些collection，就像我们定义的所有summary op都会保存在name=tf.GraphKeys.SUMMARIES。这样，tf.get\_collection\(tf.GraphKeys.SUMMARIES\)就会返回所有定义的summary op

  * placeholder

    是占位符号,暂时存储变量.从外部传入 data, 使用字典传入.
* 数据结构   Rank指数据的维度;shape 指tensor 每个维度的数据个数; Data type 指单个数据的类型,浮点整形等; &lt;br&gt;
  * Variables &lt;br&gt;在训练模型时保存于更新参数.&lt;br&gt;
  * placeholders 与 feed\_dict &lt;br&gt;定义一张 graph 时候,有时候不需要计算的值,比如输入数据,开始并没有值.所以需要这两个函数的帮助.tf.placeholder\(dtype,shape=None,name=None\)
* 初始化常见操作例子

  tf.get\_variable\(“vname”\)方法，在创建变量时，如果这个变量vname已经存在，则，直接使用这个变量，如果不存在，则重新创建；

  而tf.Variable\(\)在创建变量时，一律创建新的变量，如果这个变量已存在，则后缀会增加0、1、2等数字编号予以区别。

  这样做的目的是，搭配上不同的作用域类型，可以实现变量共享机制。

  ```text
  tf.get_variable(   #创建变量
    name,#The name of the new or existing variable.
     shape=None,
     dtype=None,
     initializer=None,
     regularizer=None,
     trainable=True, # True: 把变量加入 graph collection GraphKeys.TRAINABLE_VARIABLES
     collections=None,
     caching_device=None,
     partitioner=None,
     validate_shape=True,
     use_resource=None,
     custom_getter=None,
     constraint=None
  )
  ```

  TF中，有两种不同类型的作用域类型：

  1. 命名域 \(name scope\)，通过tf.name\_scope 或 tf.op\_scope创建；
  2. 变量域 \(variable scope\)，通过tf.variable\_scope 或 tf.variable\_op\_scope创建；

 这两种作用域，对于使用tf.Variable\(\)方式创建的变量，具有相同的效果，都会在变量名称前面，加上域名称。然而，对于通过tf.get\_variable\(\)方式创建的变量，只有variable scope名称会加到变名称前面，而name scope不会作为前缀。

```text
 #定义变量
state =tf.Variable(0, name='counter')
Weights =tf.Variable(tf.random_uniform([1], -1.0, 1.0))
biases =tf.Variable(tf.zeros([1]))
 #定义常量
matrix1 =tf.constant([[3,3]])
matrix2 =tf.constant([[2],
                        [2]])
```

 ​

### 函数记录

* `tf.assign(x,y)`:把 x 的值变为 y 的值.
* `tf.constant_initializer(0.001)`:常用来初始化偏置.
* `tf.get_collection(key,scope=None)`

  从一个指定集合中取出全部变量,是一个列表. Collection 是全局存储机制,不受到变量名生存空间的影响.

* `tf.gradients`:计算梯度

  ```text
  tf.gradients(
    ys,  #一个 tensor,被微分
    xs,  #一个 tensor,用来微分的
     grad_ys=None, #一个 tensor 列表,与 ys 长度一致.保持初始梯度,
     name='gradients', #自动默认一个这个名字
     colocate_gradients_with_ops=False,
     gate_gradients=False,
     aggregation_method=None,
     stop_gradients=None
  )
  # 返回 tensor 列表,长度是 len(xs) ,其中每个 tensor 是 sum(dy/dx) for y in ys
  # A list of sum(dy/dx) for each x in xs.
  ```

* `tf.layers.dense` :layers 模块提供 API, 构建神经网络.

  `conv2d()`。构造二维卷积层。获取过滤器的数量，过滤内核大小，填充和激活功能作为参数。

  `max_pooling2d()`。使用max-pooling算法构建二维池化层。将过滤器大小合并为一个参数。

  `dense()`。构造一个致密层\(全连接层\)。将神经元数量和激活函数作为参数。

  ```text
  tf.layers.dense(
    inputs,   #tensor input
    units,#Integer or Long, dimensionality of the output space.
     activation=None,#None to maintain a linear activation.
     use_bias=True,
     kernel_initializer=None,#Initializer function for the weight matrix. If None (default), weights are initialized using the default initializer used by tf.get_variable.
     bias_initializer=tf.zeros_initializer(), #Initializer function for the bias.
     kernel_regularizer=None, #Regularizer function for the weight matrix.
     bias_regularizer=None, #Regularizer function for the bias.
     activity_regularizer=None, #Regularizer function for the output.
     kernel_constraint=None,#An optional projection function to be applied to the kernel after being updated by an Optimizer
     bias_constraint=None,#An optional projection function to be applied to the bias after being updated by an Optimizer.
     trainable=True,#if True also add variables to the graph collection GraphKeys.TRAINABLE_VARIABLES
     name=None, #层的名字
     reuse=None#whether to reuse the weights of a previous layer by the same name.
  )
  #Output tensor the same shape as inputs except the last dimension is of size units.
  ```

* `tf.placeholder(dtype,shape=None,name=None)`

  此函数可以理解为形参,用于定义过程,执行的时候再赋具体值.

  数据类型:常用的是 tf.float32或64,string 等;shape 默认是 none, 就是一维值,\[None,3\]表示列是3,行不确定.

  返回一个张量,张量必须在使用句柄的情况下赋值,不可以直接求值.

* `tf.reduce_mean(input_tensor, reduction_indices=None, keep_dims=False, name=None)`     在输入张量的某个维度上进行求平均值,得出结果为一个标量数据. 第二个为某个维度
* `tf.train` `tf.contrib.learn` `tf.nn` 机器学习 API :

  `tf.train.Optimizer`:优化类,如梯度下降,动量更新等等.

  contrib 是第三方 API; nn 是神经网络常用的层.

  `tf.contrib.layers.xavier_initializer()`: 权重初始化函数,用来保持每一层梯度大小都差不多,返回初始化权重矩阵.

* `tf.train.RMSPropOptimizer.apply_gradients()`

  ```text
  apply_gradients(
    grads_and_vars,  #list of (gradient,variable)
     global_step=None,
     name=None
  )# returns: an Operation that applies the specified gradients,
  ```

* `tf.variable_scope(name_or_scope, reuse=None, initializer=None)`和 `tf.name_scope(name)`

  前者:为变量和节点创建名称空间. 在程序其他部分可使用tf.get\_variable提取变量.而在重复使用的时候,代码中需要强调`scope.reuse_variables()`, 否则系统将会报错, 以为你只是单纯的不小心重复使用到了一个变量.

  后者:为节点创建名称空间.

* ​

### Tensorboard

* 在 tensorboard 上添加显示自定义的变量 ⭐️

  ```text
  result =tf.Summary(value=[
  tf.Summary.Value(tag='name1',simple_value=自定变量1),
  tf.Summary.Value(tag='name2',simple_value=自定变量2)])
  ...
  writer.add_summary(result,step)
  ```

  把 writer 定义在外部, 上面这段代码可以在任意处像 graph 中加添加数据,堪称完美级!!!

* 一段参考代码

  ```text
  def variable_summaries(var):
    with tf.name_scope('summaries'):
        mean =tf.reduce_mean(var)
        tf.summary.scalar('mean', mean)
        stddev =tf.sqrt(tf.reduce_mean(tf.square(var -mean)))
        tf.summary.scalar('stddev', stddev)
        tf.summary.scalar('max', tf.reduce_max(var))
        tf.summary.scalar('min', tf.reduce_min(var))
        tf.summary.histogram('histogram', var)
  ''''''
  x =tf.placeholder(tf.float32, [None, 784])
    with tf.name_scope('weights'):
        W =tf.Variable(tf.zeros([784, 10]))
        variable_summaries(W)
    with tf.name_scope('biases'):
        b =tf.Variable(tf.zeros([10]))
        variable_summaries(b)
    with tf.name_scope('Wx_plus_b'):
        V =tf.matmul(x, W) +b
        tf.summary.histogram('pre_activations', V)
    with tf.name_scope('softmax'):
        y =tf.nn.softmax(V)
        tf.summary.histogram('activations', y)
       
  #
  distribution 显示的是取值范围;historgram 显示更细节的取值概率信息
  ```

  ​

* 基本操作

  * tf.summary

    summary 是对网络中 tensor 取值进行监测的一种 Operation, 不影响数据流本身.

    * tf.summary.scalar 记录标量: tf.summary.scalar\(tags, values, collections=None, name=None\)

      ```text
      tf.summary.scalar(
        name,
        tensor,#A real numeric Tensor containing a single value.
        collections=None,
        family=None
      )
      ```

    * tf.summary.histogram 记录数据直方图: tf.summary.histogram\(tag, values, collections=None, name=None\)
    * tf.summary.distribution 记录数据的分布图
    * tf.summary.image 记录图像数据: tf.summary.image\(tag, tensor, max\_images=3, collections=None, name=None\)

  * tf.summary.merge\(inputs, collections=None, name=None\)

    tf.summary.merge\_all 将所有 summary 节点合并成一个节点,只要运行这个节点,就能产生之前所有的 summary data. 不需要单独run 每个 Op.

  * 使用 tf.summary.FileWriter 将运行后输出的数据保存到本地.  
  * 看图: 圆圈代表常量\(const\);椭圆代表操作节点\( Op\) ;圆角方框代表子图;边代表张量的流向,边上的标记代表张量的形状,

    |  |  |
    | :--- | :--- |
    |  |  |
    |  |  |
    |  |  |
    |  |  |
    |  |  |
    |  |  |
    |  |  |

  ​

* 概念

  * histogram:

   统计 Tensor 的取值分布. Distribution 显示取值范围; histogram 中显示细节的取值概率信息.二者是对同一数据的不同方式展现.

  * name\_scope\(\)

    保证数据流图简洁,将一些子图归类为一个子节点. 管理节点.

* 输出参数图表基本代码

```text
# step1  本段代码展示输出图表的基本方法
withtf.name_scope('layer_name')
  withtf.name_scope('weights')
    Weights=...
    tf.summary.histogram('name',Weights) # 把 Weights 加到 histogram 中

withtf.name_scope('loss')
  loss=...
  tf.summary.scalar('loss',loss) # 把 loss 加到 scalar 中展示
  
#  step2  融合节点,写入 log
merged=tf.summary.merge_all()
writer=tf.summary.FileWriter('logs/',sess.graph)

# step3 在训练或学习过程中,每过一定步数,记录一下数据 
result=tf.sess.run(merged,feed_dict={,})  #字典中数据与训练的输入数据一样
writer.add_summary(result,步数)
```

### Error记录

* 重复运行程序时出错

  ```text
  ValueError: Variable conv1/weights already exists, disallowed. Did you mean to setreuse=True inVarScope? Originally defined at:...
  ```

  解决办法:在程序段前加  

  ```text
  tf.reset_default_graph()
  ```

  ​

