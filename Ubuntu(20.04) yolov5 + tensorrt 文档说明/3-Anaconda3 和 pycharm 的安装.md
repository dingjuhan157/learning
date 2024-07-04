## Anaconda3 和 pycharm 的安装               （ubuntu20.04）



### 1.安装Anacond3。

首先在home目录新建一个文件夹anaconda

官方下载地址：https://blog.csdn.net/weixin_46269422/article/details/127965528

清华源下载地址：https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/

下载对应的版本的 .sh 文件

1.1 创建一个anaconda  目录，将下载好的 .sh 文件移动到该目录下

1.2 进入终端，使用命令：	

```shell
bash Anaconda3-2022.10-Linux-x86_64.sh
```

1.3 点击回车，连续按下几次空格键

1.4 配置安装路径。

​			一般情况下，为了让其他用户也可以使用anaconda 的环境，安装路径不要使用默认的安装路径。 自己创建目录作为安装路径。



最后输入no或者yes安装就完成了
（如果选择了yes每次打开终端会自动执行conda activate root命令，这样的话，启动虚拟机shell命令前面出现(base)字样，可以用conda deactivate回去，如果选择了no，就需要我们手动的配置环境变量）（如果你选择了yes重新打开一个终端就可以使用了）

1.5 修改环境变量
			将anaconda添加到用户环境变量中去，这样不管我们在哪个目录下都可以运行这个命令了
			使用命令打开文件，如果不能保存的话，可以在前面加上sudo打开文件
						vim ~/.bashrc
			在文件的最下面添加以下内容

```shell
export PATH="/home/name/anaconda3/bin:$PATH"    #填写自己的安装路径
```



1.6 刷新配置文件：		

```shell
source ~/.bashrc
```



1.7 查看一下anaconda的版本，如果查到了就是安装完成了



```shell
conda --version
```















### 2.pycharm 的安装。

a.下载地址：

https://www.jetbrains.com/pycharm/download/#section=linux

![image-20230406172316908](.\3\3-1.png)

b.将下载好的安装包，移动到创建好的目录下

或者可以直接使用 —C 指定解压的目录

```shell
tar -zxvf pycharm-community-2022.2.1.tar.gz -C /home/yangjun/pycharm
```

c.解压后的文件名太长，可以重命名一下

```shell
mv pycharm-community-2022.2.1 pycharm-2022.2
```

e.安装pycharm:

```shell
cd pycharm-2022.2/bin
sh ./pycharm.sh
```

依次点击以下：

![img](.\3\3-2.png)

​					![img](.\3\3-3.png)

f、安装完成，点击Create Desktop Entry   （创建桌面快捷方式）

![img](.\3\3-4.png)