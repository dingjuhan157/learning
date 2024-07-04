# yolov5-6.2 进行环境的安装及模型训练。

安装好Anaconda之后，我们就可以拉去代码：

## 1.拉去代码

​	1.1 yolov5-6.2 下载地址：https://github.com/ultralytics/yolov5/tree/v6.2

​	**注:	这里拉去的yolov5 版本要跟后面使用的Tensorrtx 的版本一定要对应，不然会出现问题**



![image-20230406101129745](.\4\4-1.png)

1.2 通过命令拉去代码

git clone https://github.com/ultralytics/yolov5.git

![image-20230406101431373](.\4\4-16.png)



## 2.创建所需环境。

### 2.1 创建虚拟环境

![image-20230406102220801](.\4\4-17.png)



### 2.2 安装pytorch 

​	根据yolov5-6.2 中torch 的版本，去pytorch官网 查看  （要满足项目中torch 版本要求）

**![image-20230406102455501](.\4\4-18.png)**

**根据项目中torch的需求，然后根据cuda 版本，选择对应的链接进行安装。**（pytorch 更新的是最慢）

pytorch 地址：https://pytorch.org/get-started/previous-versions/

![image-20230406103259428](.\4\4-3.png)

2.2.1 使用命令安装pytorch   （**安装之前一定要切换到对应的虚拟环境**）

在Linux 中一般是使用pip 进行安装，在win 中一般是使用conda 命令进行安装

![image-20230406104553609](.\4\4-4.png)

2.2.2 安装项目所需要的依赖环境  （**必须要切换到对应的虚拟环境，进入到项目目录中**） 在.txt文件中将上步安装的torch 进行注释。

![image-20230406105120438](.\4\4-5.png)

2.2.3 通过命令查看安装的三方库

![image-20230406105333759](.\4\4-6.png)

## 3.进行模型的训练。

3.1 用pyrcharm 打开yolov5-6.2 的项目

![image-20230406105809871](.\4\4-7.png)

3.2 pycharm 中指定虚拟环境





3.3 数据集准备预训练模型文件。

​		3.3.1利用labelimg标注数据和数据的准备

​		3.3.2 数据最好放在最外一级目录中，然后数据集的目录格式如下图所示。一定要严格按我的格式来，否则非常容易出问题

​		![image-20230406113112118](.\4\4-8.png)

​		3.3.3 下载预训练模型文件（**预训练模型的文件要跟项目版本要一致**）

​				下载预训练模型文件（根据自己的实际情况下载模型文件）。将下载好的模型文件放到yolov5-6.2 的目录下

​				地址：

​				![image-20230406113233186](.\4\4-2.png)



3.4 加载环境，训练模型。

​	3.4.1 加载虚拟环境。

![image-20230406111545872](.\4\4-9.png)



3.5 修改参数文件，进行模型训练。

​	3.5.1 复制data VOC.yaml 文件为aa.yaml 。 aa.yaml 中指定数据集。

![image-20230406163600569](.\4\4-10.png)

3.5.2  复制models 目录下的yolov5s.yaml文件为同级目录下的cs.yaml。   (这里面只修改 nc)

![image-20230406163750410](.\4\4-12.png)



3.5.3 修改train.py 文件中的

--weights   (下载好的预训练模型)

-- cfg          (指定3.5.2中复制的cs.yaml)

--data        (指定3.5.1中复制的aa.yaml)

指定这三个参数之后，就可以运行 train.py 文件

![image-20230406163505797](C:\Users\heyuanli\AppData\Roaming\Typora\typora-user-images\image-20230406163505797.png

![image-20230406163339806](.\4\4-13.png)



3.5.4 启用tensorbord查看参数
         yolov5里面有写好的tensorbord函数，可以运行命令就可以调用tensorbord，然后查看tensorbord了。首先打开pycharm的命令控制终端，输入如下命令，就会出现一个网址地址，将那行网址复制下来到浏览器打开就可以看到训练的过程了

tensorboard --logdir=runs/train



3.5.5  训练过程中常见的错误：

a.GPU显存溢出的报错![image-20230406165324754](.\4\4-11.png)

解决的方法是：

调小一下两个参数：

![image-20230406165524822](C:\Users\heyuanli\AppData\Roaming\Typora\typora-user-images\image-20230406165524822.png)

![image-20230406165548882](C:\Users\heyuanli\AppData\Roaming\Typora\typora-user-images\image-20230406165548882.png)



b.以上都设置好了就可以训练了。但是pycharm的用户可能会出现如下的报错。这是说明虚拟内存不够了。

![image-20230406165612041](.\4\4-14.png)

解决的方法：

将 utils 下的dataloaders.py 中的num_workers改为0.

![image-20230406165927388](.\4\4-15.png)





至此，就可以运行train.py函数训练自己的模型了