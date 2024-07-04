# 							Ubuntu(20.04) 从系统安装到(yolov5-6.2)模型训练								

## 一.Ubuntu 双系统的安装。

## 二.显卡驱动，cuda , cudnn 的安装。

## 三. Anaconda3 和 pychar 的安装。

## 四.拉取 yolov5-6.2 代码并训练模型。

## 五. Tensorrt opencv cmake安装和配置。

## 六.Tensorrtx 代码的部署，及.pt文件转换为 .os 模型文件。

## 环境版本：

​	ubuntu 20.04

​	显卡驱动                                nvidia-smi

​	cuda   11.3.1                         nvcc -V

​	cudnn  8.2.1						  cat /usr/local/cuda-11.3/include/cudnn_version.h | grep CUDNN_MAJOR -A 2

​	Tensorrt 8.0.3.4					

​	opencv 4.5.4                         opencv_version

​	cmake 3.25.3						cmake --version

​					（cuda cudnn Tensorrt opencv 版本一定要对应，cmake版本没有硬要求，任意版本都可以的）

​	yolov5    6.2

​	tensorrtx 6.2

​						(拉去代码的时候  yolov5 和 tensorrtx 版本要对应)

### 

```python
常用的网页链接：
yolov5 + tensorrt : https://blog.csdn.net/uzumakinarutoka/article/details/127917403

cuda下载：https://developer.nvidia.com/?destination=node/899897%3Ftarget_os%3DLinux%26target_arch%3Dx86_64%26Distribution%3DUbuntu%26target_version%3D20.04%26target_type%3Drunfile_local&autologout_timeout=1
cudnn下载:https://developer.nvidia.com/rdp/cudnn-archive

Tensorrt 下载：https://developer.nvidia.com/nvidia-tensorrt-8x-download
安装：https://www.cnblogs.com/wangtianning1223/p/17236281.html
官网安装教程：https://docs.nvidia.com/deeplearning/tensorrt/install-guide/index.html#installing-tar

opencv下载：https://opencv.org/releases/
opecv安装：https://blog.csdn.net/Koko20211012/article/details/128192930


(cuda cudnn tensorrt opencv 版本一定要对应)

cmake 下载：https://cmake.org/download/    （版本无所谓）
cmake 安装：https://www.cnblogs.com/lurl/p/16834186.html


tensorrtx 下载地址：https://github.com/wang-xinyu/tensorrtx/tree/yolov5-v6.2
```

