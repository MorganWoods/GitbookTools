---
description: RL testbeds integration
---

# RLSimulators

> 除了 gym 之外没有一个成功安装的. 妈的.....气死我了.

## Universe 🌀

> euclidean \[/ju:'klidiən/\] 欧几里何; unstructured outdoor environments 不规则的户外环境; geometry 几何学; geography 地理学; coarse 粗糙的;rectified 改正的;stereo 立体的,立体声的,立体,立体声; collaborate 合作 v ; integrate 整合 vt ; validate 确认,使生效, 验证. Grant us permission 授予许可; archive 存档.; hub 中心;

[https://blog.openai.com/universe](https://blog.openai.com/universe) 其博客

### ➡ Intro

gym 是工具包, universe 基于 gym, 是评估,训练agent 的软件平台. 是一个开源库,  
universe 包含1000多种环境,如 flash, 网页.侠盗飞车等; Universe 的环境运行在一个 docker 容器里,然后通过 vnc 等方式来远程连接.  
Docker: 用来放应用与程序的一个容器,负责 runing 应用; 是著名的轻量级虚拟化技术,最近很火.在 windows 和 mac 上好像不能用,需要虚拟机. Docker 在线的容器平台是 Docker hub;

VNC: virtual network console 虚拟网络控制台.是一款优秀的远程控制工具软件.

Docker 命令: docker info ; docker ps 显示进程; docker images 显示镜像;

Universe 要配合 py3.5

以下任务类包装在公共可用的Docker容器中，现在就可以无需任何额外的工作马上运行：

* 通过VNC玩雅达利和CartPole游戏： ，`gym-core.Pong-v3`，`gym-core.CartPole-v0`等。
* VNC上的Flash游戏：`flashgames.DuskDrive-v0`等
* VNC上的浏览器会话（World of Bits”）：`wob.mini.TicTacToe-v0`等

### ➡ Installation for Mac

> ...  
> [https://medium.com/@alexbhandari/openai-universe-getting-started-on-mac-52d601ef9161](https://medium.com/@alexbhandari/openai-universe-getting-started-on-mac-52d601ef9161)  
> mac 的 gym 和 universe 都在 anaconda py35 环境下;

Run Universe within the Anaconda environment. Anaconda creates a open-ai environment.  
Ensure xcode command line tools were installed.  
Xcode is IDE for ios.

```text
pip install numpy incremental
brew install golang libjpeg-turbo
pip install -e .    # 安装时候出错
```

Then install universe.  
install Docker.  
**Go 语言:**是一个开源编程语言,构造简单可靠.简单,并行,有趣,迅速.对于服务端的开发很好,如游戏.

❌Failed building wheel for go-vncdriver    遇见这个错误,  通过安装 go-vncdriver 解决: [https://github.com/openai/go-vncdriver](https://github.com/openai/go-vncdriver) 参照此网站步骤解决了 ✅  
  
**libjpeg** 是开源库,关于图像解码的. **zbar** 是开源条形码二维码算法库. **zbarlight** 是前者的封装库,方便识别二维码.

又遇到问题,python 中引用失败`ImportError:dlopen(/Users/menghaw1/anaconda2/envs/py35/lib/python3.5/site-packages/fastzbarlight/_zbarlight.cpython-35m-darwin.so, 2): Symbol not found: _iconv.`   
解决办法:[https://github.com/openai/universe/issues/139](https://github.com/openai/universe/issues/139)  
brew install zbar ; 然后在安装 zarblight , 目前在更新 xcode ,然后重新来.

❌安装 zbar 失败; 问题解决, 因为 GCC 或 Clang 版本过时,需要更新他们,然后才行\(在人的帮助下完成\)  ✅

```text
brew install zbar
export LDFLAGS="-L$(brew --prefix zbar)/lib"
export CFLAGS="-I$(brew --prefix zbar)/include"
pip install zbarlight  #输入上两句之后安装成功.
```

❌[https://github.com/openai/universe/issues/139\#issuecomment-289441706](https://github.com/openai/universe/issues/139#issuecomment-289441706)  目前按照这个指导操作.  
在 import universe 时候提示错误:ImportError: No module named 'go\_vncdriver' ;   
但在安装go\_vncdriver的时候他找不到 libjpeg-turbo,可他已经安装.  
在安装 libjpeg-turbo 时候出现以下提示信息

```text
This formula is keg-only, which means it was not symlinked into /Users/menghaw1/Homebrew,
because libjpeg-turbo is not linked to prevent conflicts with the standard libjpeg.

If you need to have this software first in your PATH run:
  echo 'export PATH="/Users/menghaw1/Homebrew/opt/jpeg-turbo/bin:$PATH"' >> ~/.zshrc

For compilers to find this software you may need to set:
    LDFLAGS:  -L/Users/menghaw1/Homebrew/opt/jpeg-turbo/lib
    CPPFLAGS: -I/Users/menghaw1/Homebrew/opt/jpeg-turbo/include
For pkg-config to find this software you may need to set:
    PKG_CONFIG_PATH: /Users/menghaw1/Homebrew/opt/jpeg-turbo/lib/pkgconfig
```

手动更改了 go \_vnc 的 build 代码让他能找到 lib 文件位置 , 似乎可以运行了但是它找不到 jpeglib.h 的位置了.明天查找原因. 改回来了,重新找重装 ligjpeg 的方法,让他安装过后能被其他程序找到.  
当前 go 安在 brew 里,已经卸载 brew 的 go,还有一个是系统的.  
卸载了 libjpeg-turbo, 打算手动安装,把上面那几个参数都加上. 明天安这个

网上找的使用方法

```text
LDFLAGS = -L/var/xxx/lib -L/opt/mysql/lib
LIBS = -lmysqlclient -liconv
这就明白了。LDFLAGS告诉链接器从哪里寻找库文件，LIBS告诉链接器要链接哪些库文件。
不过使用时链接阶段这两个参数都会加上，所以你即使将这两个的值互换，也没有问题。

说到这里，进一步说说LDFLAGS指定-L虽然能让链接器找到库进行链接，但是运行时链接器却找不到这个库，
如果要让软件运行时库文件的路径也得到扩展，那么我们需要增加这两个库给"-Wl,R"

LDFLAGS = -L/var/xxx/lib -L/opt/mysql/lib -Wl,R/var/xxx/lib -Wl,R/opt/mysql/lib

如 果在执行./configure以前设置环境变量export LDFLAGS="-L/var/xxx/lib -L/opt/mysql/lib -Wl,R/var/xxx/lib -Wl,R/opt/mysql/lib" ，
注意设置环境变量等号两边不可以有空格，而且要加上引号哦（shell的用法）。那么执行configure以后，
Makefile将会设置这个选项， 链接时会有这个参数，编译出来的可执行程序的库文件搜索路径就得到扩展了。

------------------------------------------------------------------------------------------------------------------------

PS：-Wl,R在GraphicsMagick环境下，用为-R, 也就是LDFLAGS = -L/var/xxx/lib -R/var/xxx/lib

CFLAGS 或 CPPFLAGS的用法
CPPFLAGS='-I/usr/local/libjpeg/include -I/usr/local/libpng/include'

我需要
export LDFLAGS="-L/Users/menghaw1/Homebrew/opt/jpeg-turbo/lib"; 
export CPPFLAGS="-I/Users/menghaw1/Homebrew/opt/jpeg-turbo/include"; 
export PKG_CONFIG_PATH="/Users/menghaw1/Homebrew/opt/jpeg-turbo/lib/pkgconfig"; 
echo 'export PATH="/Users/menghaw1/Homebrew/opt/jpeg-turbo/bin:$PATH"' >> ~/.zshrc

修改版:
export LIBJPG="-L/Users/menghaw1/Homebrew/opt/jpeg-turbo/lib"; 
export LIBJPG="-I/Users/menghaw1/Homebrew/opt/jpeg-turbo/include"; 
export PKG_CONFIG_PATH="/Users/menghaw1/Homebrew/opt/jpeg-turbo/lib/pkgconfig"; 

```

加了之后还是一样的效果, 没用.  
把 go 卸载了.重装.  
还是 jpeg-turbo 安装的有问题.再找吧.卧槽的.❌ 

----------Sep 2, 2018-----------

Installation as [https://github.com/openai/universe-starter-agent/blob/master/README.md](https://github.com/openai/universe-starter-agent/blob/master/README.md) shows:

```text
conda create --name universe-starter-agent python=3.5  ✅
source activate universe-starter-agent   ✅

brew install tmux htop cmake golang libjpeg-turbo     ✅[1] # On Linux use sudo apt-get install -y tmux htop cmake golang libjpeg-dev

pip install "gym[atari]"   ✅
pip install universe
pip install six
pip install tensorflow
conda install -y -c https://conda.binstar.org/menpo opencv3
conda install -y numpy
conda install -y scipy
```

  
\[1\] You may wish to add the GOROOT-based install location to your PATH:  
export PATH=$PATH:/Users/menghaw1/Homebrew/opt/go/libexec/bin

### ➡ Installation for ubuntu

今天尝试在ubuntu上安装一下:  


## RoboSchool🌀

### ➡ intro

We continue to recommend the use of roboschool1 Hopper, Ant, Humanoid and Flagrun for evaluation and testing of algorithms. If you have fixes to make installation easier we'll be happy to merge it. We'll have more to share about roboschool2 in a while. Physical simulation.

{% embed data="{\"url\":\"https://blog.openai.com/roboschool/\",\"type\":\"link\",\"title\":\"Roboschool\",\"description\":\"We are releasing Roboschool: open-source software for robot simulation, integrated with OpenAI Gym.    Your browser does not support the video tag. Three control policies running on three different robots, racing each other in Roboschool. You can re-enact this scene by running agentzoo/demorace1.py. Each time you run the script,\",\"icon\":{\"type\":\"icon\",\"url\":\"https://blog.openai.com/assets/images/favicon/favicon.ico\",\"aspectRatio\":0},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://blog.openai.com/assets/images/opengraph/research/cyan.jpg?v=a52c934624\",\"width\":1200,\"height\":630,\"aspectRatio\":0.525},\"caption\":\"Blog\"}" %}

Roboschool is a long-term project to create simulations useful for research. The roadmap is as follows:

1. Replicate Gym MuJoCo environments.
2. Take a step away from trajectory-centric fragile MuJoCo tasks.
3. Explore multiplayer games.
4. Create tasks with camera RGB image and joints in a tuple.
5. Teach robots to follow commands, including verbal commands.

  
The list of Roboschool environments is as follows:

* RoboschoolInvertedPendulum-v0
* RoboschoolInvertedPendulumSwingup-v0
* RoboschoolInvertedDoublePendulum-v0
* RoboschoolReacher-v0
* RoboschoolHopper-v0
* RoboschoolWalker2d-v0
* RoboschoolHalfCheetah-v0
* RoboschoolAnt-v0
* RoboschoolHumanoid-v0
* RoboschoolHumanoidFlagrun-v0
* RoboschoolHumanoidFlagrunHarder-v0
* RoboschoolPong-v0

To obtain this list: `import roboschool, gym; print("\n".join(['- ' + spec.id for spec in gym.envs.registry.all() if spec.id.startswith('Roboschool')]))`

Agent Zoo  
We have provided a number of pre-trained agents in the `agent_zoo` directory.

To see a humanoid run towards a random varying target:

```text
python $ROBOSCHOOL_PATH/agent_zoo/RoboschoolHumanoidFlagrun_v0_2017may.py
```

To see three agents in a race:

```text
python $ROBOSCHOOL_PATH/agent_zoo/demo_race2.py
```

### ➡ Installation for Mac

2018年09月04日10:57:15     
installed it in the py35 virtual conda-env. gym also in this env.  
meet this error: [https://github.com/openai/roboschool/issues/47](https://github.com/openai/roboschool/issues/47)  cannot solve.  
安装 qt 与 gcc 中...; 之后把 qt 路径加进去.在试试吧... 唉,擦得.  
2018年09月05日09:03:48  
QT5的 directory: /Users/menghaw1/Homebrew/opt/qt/lib/pkgconfig   
🚫.sucks! 愁死我了,妈的.

## Gym 🌀

### ➡ Intro

Gym blog: [https://gym.openai.com/envs](https://link.jianshu.com/?t=https%3A%2F%2Fgym.openai.com%2Fenvs)  
环境包括: Atari, Box2D, Classic control, MuJoCo, Robotics, Toy text.

* 使用环境

  ```text
  import gym
  env =gym.make('CartPole-v0')
  env.reset()
  fori_episode inrange(20):
    observation =env.reset()
     fort inrange(100):
        env.render() #显示模拟界面
        print(observation)
        action =env.action_space.sample()
        observation, reward, done, info =env.step(action)
         ifdone:
            print("Episode finished after {} timesteps".format(t+1))
            break
  ```

* 环境汇总

  > [https://gym.openai.com/envs/\#classic\_control](https://gym.openai.com/envs/#classic_control) This is the birds-eye view

  ​

* 常用函数介绍

  ```text
  step()# 返回四个值,是 observation,reward,done,info; 其中 info 是调试用的,不能参考这个值来学习.
  reset()# 返回初始的 observation.
  ​
  '''显示动作空间维数和观测空间维数'''
  print(env.action_space)   # 对于 cartpole 的空间
  #> Discrete(2)
  print(env.observation_space) 
  #> Box(4,)
  ​
  '''有效的观测是4个数的数组,可以查看 box 的边界'''
  print(env.observation_space.high)
  #> array([ 2.4       ,         inf, 0.20943951,         inf])
  print(env.observation_space.low)
  #> array([-2.4       ,       -inf, -0.20943951,       -inf])
  ```

  env = gym.make\(‘CartPole-v0’\)   创建环境

  env.reset\(\)    初始化作用,或者每次新episode 的重启

  env.render\(\)

  cartpole 环境目录在 gym/gym/envs/下;

  一次尝试称之为一条轨迹或者 episode. 每次尝试都达到终止状态;

  step\(\) 函数与环境交互用的

  马尔科夫过程包括:状态空间/动作空间,回报函数,状态转移概率.

  下面重点讲一讲如何将建好的环境进行注册，以便通过gym的标准形式进行调用。其实环境的注册很简单，只需要３步：

  第一步：将我们自己的环境文件（我创建的文件名为grid\_mdp.py\)拷贝到你的gym安装目录/gym/gym/envs/classic\_control文件夹中。（拷贝在这个文件夹中因为要使用rendering模块。当然，也有其他办法。该方法不唯一）

  第二步：打开该文件夹（第一步中的文件夹）下的\_\_init\_\_.py文件，在文件末尾加入语句：

  from gym.envs.classic\_control.grid\_mdp import GridEnv

  第三步：进入文件夹你的gym安装目录/gym/gym/envs，打开该文件夹下的\_\_init\_\_.py文件，添加代码：

  register\(

  id='GridWorld-v0',

  entry\_point='gym.envs.classic\_control:GridEnv',

  max\_episode\_steps=200,

  reward\_threshold=100.0,

  \)

  第一个参数id就是你调用gym.make\(‘id’\)时的id,　这个id你可以随便选取，我取的，名字是GridWorld-v0

  第二个参数就是函数路口了。

  后面的参数原则上来说可以不必要写。

## ​Gazebo 🌀

bash 文档的代码相当于都执行在终端上

\[-f file\]  若 file 存在且是一个普通文件 则为真

括号同上: -d DIR : 若 DIR 存在且是一个目录,为真

Rospack find packagename

## Turtlebot3 🌀

remotePC ip : 192.168.43.245        10.100.34.151                   MASTER  
Turtlebot ip: 192.168.43.166           10.100.42.143   53.19     HOSTname  
turtlebot 倒数第二个 ip 是电脑的 ip  
打开 ip 文件命令: gedit ˜/.bashrc    之后  source  

Bringup 章节  
PC: roscore  
Turtlebot: roslaunch turtlebot3\_bringup turtlebot3\_robot.launch  全启动  
只启动核心: roslaunch turtlebot3\_bringup turtlebot3\_core.launch  
PC: export TURTLEBOT3\_MODEL=burger  
roslaunch turtlebot3\_bringup turtlebot3\_model.launch

Teleoperation章节  
PC 上启动控制操作: roslaunch  turtlebot3\_teleop turtlebot3\_teleop\_key.launch

SLAM 章节  
PC   :  export TURTLEBOT3\_MODEL=burger  
 roslaunch turtlebot3\_slam turtlebot3\_slam.launch  
可视化:  rosrun rviz rviz -d \`rospack find turtlebot3\_slam\`/rviz/turtlebot3\_slam.rviz  
存地图: roslaunch turtlebot3\_teleop turtlebot3\_teleop\_key.launch  
存地图:rosrun map\_server map\_saver -f ~/map  


常用 ros\ 命令  
rqt\_graph  
清单文件中 版本2把  rundepend 改成 execdepend  
rosclean check 检查日志占用的内存,在超过1G 的时候会在 roscore 和 roslaunch 中提醒,  
rosclean purge 可以删除这些日志  
节点,话题,服务和参数统称为计算图源,graph resource name  
连接 rospi  
Ssh wu@172.24.1.1  
Password  raspberry  
查看 ros 位置   printenv \| grep ROS  
Ros kill other  roscore ; killall -9 roscore  
 rostopic list  
 rosparam list  参数  
 rosservice list  
 rqt\_graph  节点图

