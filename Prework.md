# 搬运一些施工必要材料
* 安装java
* 安装GoGui
* 安装GnuGo
* 安装MuGo
* GnuGo常用命令

## 安装java
如果ubuntu上已经有java的话可以跳过这一步，没有的话需要去安装一下并配置好环境变量

可以使用下面的command检查是否装好了java：

```Bash
java -version
```

下载地址：http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
我在ubuntu上下载的是jdk-8u152-linux-x64.tar.gz

## 安装GoGUI
Google上能找到的相关网站是这个：https://senseis.xmp.net/?Gogui

但是这个网站给出的链接下载的是.tar.gz文件，安装时会提示缺少lib文件夹，所以建议直接下载repo上的.zip文件

* 解压.zip文件
```Bash
unzip gogui-1.4.9.zip
```

* 运行install.sh文件
```Bash
sudo ./install.sh -j JAVA_HOME
```
注意这一步因人而异，install.sh 默认 JAVA_HOME=/usr. 如果你的JAVA_HOME和默认的不一致的话会导致安装失败。可以用下面这个command找到你的JAVA_HOME:
```Bash
which java
```
在成功安装java后应该会显示：JAVA_HOME/bin/java

如果以上步骤都没有问题的话，这里安装是非常快的，但是安装成功也不会有提示...可以在terminal中输入以下command来确认，出现GoGui的界面则安装成功
```Bash
gogui
```

## 安装GnuGo
输入以下command直接安装：
```Bash
sudo apt-get install gnugo
```

## 安装MuGo
MuGo是用python3写成的部分复现AlphaGo的围棋AI，原repo：https://github.com/brilee/MuGo

直接下载release中的版本，直接clone整个repo的话需要重新训练网络，而release中的版本有一个训练好的模型

Ubuntu下默认的python版本是python2，README中的几个指令需要相应地改成pip3：
```Bash
pip3 install -r requirements.txt
```
同理运行时指定python3 运行
```Bash
python3 main.py gtp policy --read-file=saved_models/20170718
```
其中 saved_models/20170718 是release版本中训练好的模型参数

## GnuGo常用命令
### 在GnuGo中导入一个 Go Engine
在terminal中打开GoGui. Program => New Program 之后按照提示做即可

### 让两个Go AI 在gogui中对局
以MuGo和GnuGo为例，每个程序需要指定启动命令
```Bash
BLACK="gnugo --mode gtp"
WHITE="python3 main.py gtp policy --read-file=saved_models/20170718"
TWOGTP="gogui-twogtp -black \"$BLACK\" -white \"$WHITE\""
gogui -program "$TWOGTP" -computer-both -auto
```

### 让两个Go AI 对局并分析数据
同样以MuGo为例，关于-analyze更多可以参考：https://www.mankier.com/1/gogui-twogtp

文档中给出的命令会自动在当前路径下生成.sgf文件，对局多的时候会出现一大堆文件，可以用一个文件夹来保存所有对局数据。在保存数据的路径下运行下面指令即可：
```Bash
BLACK="gnugo --mode gtp"
WHITE="python3 ../main.py gtp policy --read-file=../saved_models/20170718"
gogui-twogtp -black "$BLACK" -white "$WHITE" -games 10 -size 19 -alternate -sgffile gnuvsmugo -auto

gogui-twogtp -analyze gnuvsmugo.dat
```
对局结果可以在.html文件中看到，“B+3.5”指黑棋赢3.5目，“B+R”指黑棋胜，白棋投降

