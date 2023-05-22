# YOLOV5Project
YOLOv5代码本地训练模型
本文记录自己本地使用YOLOv5算法训练识别安全帽和人脸的过程，以供以后学习参考。
具体流程可以查看我的博客：https://blog.csdn.net/Lost_The_Mind/article/details/130583159?spm=1001.2014.3001.5501

一、学习资源
1、B站炮哥保姆级YOLOv5本地训练模型讲解
强推：
https://www.bilibili.com/video/BV1f44y187Xg/?p=6&spm_id_from=pageDriver&vd_source=2fa09a0655d11f6cfae7287ba7e9df31

2、YOLOv5源码
https://github.com/ultralytics/yolov5/tree/v5.0
YOLOv5源码下载，本次所有实验都是使用YOLOv5-5.0这个版本

3、数据集的下载
YOLOv5算法采用的是VOC数据集，所以要对原始数据集进行标注处理，然后划分数据集为训练集与测试集。其中会使用labelImg工具对图像进行打标签的操作以及格式转换。
这里是已经划分好的数据集，具体的图像处理与数据集划分炮哥的博客中都有详细介绍。
炮哥 YOLOv5教程博客：https://blog.csdn.net/didiaopao/category_11321656.html?spm=1001.2014.3001.5482

数据集：
夸克网盘：https://pan.quark.cn/s/af9d304b2a00 提取码：QZUC
百度网盘：https://pan.baidu.com/s/1SKkv19bk6xwDME0KgfVGhQ 提取码：pVG2

二、算法训练流程
1、利用Anaconda安装pytorch+pycharm，安装CUDA和CUDNN
2、利用labeling工具标注VOC格式的数据集以及数据集的划分
使用labeling工具可以对自己的数据集进行标注处理，然后再使用相应python脚本将比标注的xml文件转换为txt格式文件，具体流程细节炮哥博客有详细介绍这里就不多做赘述。
上述所提供的数据集已经包含了划分好的数据集，包含安全帽和人脸两种标注可以直接使用。

3、使用YOLOv5代码本地训练模型
（1）项目克隆
首先，要从github官网上克隆YOLOv5的源码，使用的是YOLOv5-5.0这个版本的源码。然后使用一款IDE打开这个项目
（2）环境与依赖的安装
在项目中有一个requirements.txt文件，打开requirements.txt这个文件，可以看到里面有很多的依赖库和其对应的版本要求。我们打开pycharm的命令终端，在中输入如下的命令，就可以安装了。
pip install -r requirements.txt
（3）数据集和预训练权重的准备
炮哥博客：https://blog.csdn.net/didiaopao/article/details/120022845
这篇博客完整的讲述了如何使用labeling标注数据集以及数据集的划分。
本地YOLOv5的在本地训练如果使用随机值开始训练的话，必须花费好多轮迭代才能使得测试集的mAP值达到一个比较好的效果。 一般为了缩短网络的训练时间，并达到更好的精度，我们一般加载预训练权重进行网络的训练。YOLOv5-5.0提供了好几个版本的预训练权重文件，可以在这个网址进行下载：https://github.com/ultralytics/yolov5/releases，这里我们所以使用的是yolov5s.pt这个预权重文件。
（4）使用准备好的数据集本地训练模型
   1）首先将数据集文件VOC2007放在YOLOv5-5.0这个项目的文件夹中，将与预训练权重文件yolov5s.pt放在该项目文件夹下的weights文件夹下。
   2）修改数据配置文件与模型配置文件
   将数据文件夹data目录下的voc.yaml文件重新复制一份并重命名为hat.yaml
   3）训练自己的模型
   完成上述修改后我们即可开始训练模型，打开train.py文件。训练自己的模型需要修改如下几个参数就可以训练了。首先将weights权重的路径填写到对应的参数里面，然后将修好好的models模型的yolov5s.yaml文件路径填写到相应的参数里面，最后将data数据的hat.yaml文件路径填写到相对于的参数里面。这几个参数就必须要修改的参数。
   4）启用tensorbord查看参数
   yolov5里面有写好的tensorbord函数，可以运行命令就可以调用tensorbord，然后查看tensorbord了。首先打开pycharm的命令控制终端，输入如下命令，就会出现一个网址地址，将那行网址复制下来到浏览器打开就可以看到训练的过程了。
（5）推理测试
   找到主目录下的detect.py文件，这里需要将刚刚训练好的最好的权重传入到推理函数中去，然后填人图像或者视频的路径就可以对图像视频进行推理了。
   
