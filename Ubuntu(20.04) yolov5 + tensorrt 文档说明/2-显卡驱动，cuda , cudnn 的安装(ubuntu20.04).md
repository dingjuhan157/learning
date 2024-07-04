## 									显卡驱动，cuda , cudnn 的安装(ubuntu20.04)



### 一、显卡驱动安装

### 二、cuda 安装  （11.3.1）

### 三、cudnn 的安装  



### 一、显卡驱动安装：

**只有集显，没有独显的使用一下安装驱动方式，直接插集显视频接口操作即可：**

安装显卡驱动所需要的必要软件包：

```shell
apt-get update
apt-get install gcc
apt-get install g++
apt-get install make
```



NVIDIA[显卡驱动](https://so.csdn.net/so/search?q=显卡驱动&spm=1001.2101.3001.7020)可以通过指令`sudo apt purge nvidia*`删除以前安装的NVIDIA驱动版本，重新安装



#### 1、 前期准备

禁用[BIOS](https://so.csdn.net/so/search?q=BIOS&spm=1001.2101.3001.7020)的secure boot，即disable它，如果不关闭，使用第三方源安装显卡驱动会安装后不能使用。

#### 2、**禁用nouveau**

1）创建文件，如果没有下载[vim编辑器](https://so.csdn.net/so/search?q=vim编辑器&spm=1001.2101.3001.7020)，将vim换成gedit即可

```shell
$ sudo vim /etc/modprobe.d/blacklist-nouveau.conf
```

2） 在文件中插入以下内容，将nouveau加入黑名单，默认不开启

```
blacklist nouveau
options nouveau modeset=0
```

3） 输入以下命令使禁用生效然后重启

```
$ sudo update-initramfs -u
$ sudo reboot
```

4）重启后验证

```
lsmod | grep nouveau
```

**如果回车后无反应，则禁用成功**



#### 3、 下载驱动文件

1） 下载地址：https://www.nvidia.cn/Download/index.aspx



2） 执行命令 

```shell
chmod a+x NVIDIA_Linux-x86_64_525.105.17.run

sh NVIDIA_Linux-x86_64_525.105.17.run -no-opengl-files
```



出现缺少什么依赖，就安装什么依赖



安装成功之后，输入nvidia-smi 进行查看，并确定cuda 版本

```shell
nvidia-smi
```



![image-20230413114904576](.\2\0_1.png)

​                                                                                                                     2-1





**既有集显有独显的，先用集显安装好系统，在切换到独显，下载好驱动文件，禁用默认的系统自带的驱动，然后安装驱动。**



#### 4、注意（一定要有禁用内核的操作）：

ubuntu  安全策略问题，系统重启后，会自动检查更新内核版本。上一步我们装了显卡驱动，内核版本和显卡驱动版本不对应会出现显卡不能用的情况。

直接禁用内核重启自动更新就好了。

完全禁止ubuntu 内核更新：

1. 使用uname -a 查看当前内核版本：
   ![image-20230413114904576](.\2\11.png)

2.修改一下两个文件：

sudo vi /etc/apt/apt.conf.d/10periodic

sudo vi /etc/apt/apt.conf.d/20auto-upgrades

后部分全部改为 ”0“

![image-20230413114904576](.\2\12.png)

3.使用dkms 查看显卡驱动和内核对应关系

```shell
dkms status
```

显卡驱动为：525.147.05

内核版本为：5.15.0-92-generic

![image-20230413114904576](.\2\13.png)



4. 使用 reboot 进行重启

### 二、cuda 安装

#### 1、下载地址：https://developer.nvidia.com/cuda-toolkit-archive

#### 2、在安装cuda11.x 之前需要安装一些依赖

```shell
sudo apt-get install freeglut3-dev build-essential libx11-dev libxmu-dev libxi-dev libgl1-mesa-glx libglu1-mesa libglu1-mesa-dev
```

如果出现错误，升级仓库
根据提示，依次执行如下命令：

```
sudo apt-get update
sudo apt-get upgrade --fix-missing
```

完成后再次执行安装命令。如果还是出现一样的错误，尝试下一个方法。

![image-20230413114904576](.\2\1.png)

#### 3、拉去.run包进行安装：

***选择对应的版本***

![image-20230413114904576](.\2\1_2.png)

点击之后会跳转到这个页面

![image-20230413114904576](.\2\1.1.png)

1） 拉去.run 包

```shell
wget https://developer.download.nvidia.com/compute/cuda/11.3.1/local_installers/cuda_11.3.1_465.19.01_linux.run
```

![image-20230413115219532](.\2\2.png)

2） 进行安装

```shell
sudo sh cuda_11.0.2_450.51.05_linux.run
```

运行上面指令后，会弹出如下界面，点击`Continue`，然后再输入`accept`。

![image-20230413115625893](.\2\3.jpg)

输入 accept

![image-20230413115837468](.\2\4.jpg)

接着，如下图所示，在弹出的界面中通过Enter键，取消Driver和465.19.01的安装，然后点击Install，等待

注意：回车键作用是将 [X] 就会变成[ ]，[X]代表有，[ ]代表无。因为刚才nvidia-smi有显示的东西，因此需要将第一行的[X] Driver去掉，光标走到第一行，按回车，变成如下图所示，然后install即可。
	![image-20230413120039632](.\2\5.jpg)

过一会出现如下的图：

![image-20230413124249718](.\2\7.jpg)

会在/usr/local 中出现以下两个目录

![image-20230413124348640](.\2\6.jpg)

3）配置环境变量

CUDA安装完成后，需要配置变量环境才能正常使用。首先在终端输入sudo gedit ~/.bashrc打开如下图所示的.bashrc文件。 然后，如下图所示在.bashrc文件的最后添加以下CUDA环境变量配置信息（我从不同的文章中看到这里添加的信息不仅相同，目前还不太清楚具体含义，所以这里仅仅罗列出它们）：

```shell
export PATH=$PATH:/usr/local/cuda/bin  
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64  
export LIBRARY_PATH=$LIBRARY_PATH:/usr/local/cuda/lib64

```

或：

```shell
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64
export PATH=$PATH:/usr/local/cuda/bin
export CUDA_HOME=$CUDA_HOME:/usr/local/cuda
```

![image-20230413124551644](.\2\8.jpg)

最后，在终端输入`source ~/.bashrc`或者重新启终端使之生效。这时，我们就可以在终端输入`nvcc -V`查看CUDA的安装信息，如下图所示，至此CUDA安装成功。

![image-20230413124752967](.\2\9.jpg)

#### 3、cuda 测试

系统安装CUDA包括两个部分：NVIDIA CUDA GPU计算工具包和NVIDIA CUD示例包两个部分。 如下图所示，Ubuntu20.04系统会默认地将CUDA的NVIDIA GPU计算工具包安装到/usr/local/文件夹下面，可以看到该文件夹下多了两个文件夹cuda和cuda-11.3

对CUDA安装是否成功，需要进入NVIDIA CUDA示例包，其位于/home/用户名/NVIDIA_CUDA-11.3_Samples内，在该文件夹下打开终端，并输入make。然后进入1_Utilities/deviceQuery文件夹，并在终端执行./deviceQuery命令，如下result=PASS则表示安装成功。


![image-20230413125107021](.\2\10.jpg)



如果失败，重启电脑执行`./deviceQuery`







### 三、cudnn 安装

1） 下载地址：

https://developer.nvidia.com/rdp/cudnn-archive

![image-20230413142459463](.\2\01.png)

2）下载后将其进行解压：

![image-20230413142459463](.\2\02.png)

```shell
tar -zxvf cudnn-11.3-linux-x86-v8.2.1.32.tgz
```

3） 进入到解压后的目录，进行拷贝文件  （一定要切换到 root ）

然后，使用下面两条指令复制`cuda`文件夹下的文件到`/usr/local/cuda-11.3/lib64/`和`/usr/local/cuda-11.3/include/`中

```shell
cp cuda/lib64/* /usr/local/cuda-11.0/lib64/
cp cuda/include/* /usr/local/cuda-11.0/include/
```

4）查看cudnn 的版本

```shell
cat /usr/local/cuda/include/cudnn_version.h | grep CUDNN_MAJOR -A 2
```

![image-20230413142459463](.\2\2_1.png)
