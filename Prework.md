# Install GoGUI and GnuGo

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

## 在GoGui中导入GnuGo并与(bei)其(ta)对(xue)战(nue)
在terminal中打开GoGui.

Program => New Program 之后按照提示做即可

