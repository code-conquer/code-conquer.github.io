---
title: 使用pytorch在ImageNet上训练自定义模型
commentable: flase
Edit: 2020-3-13
mathjax: true
mermaid: true
tags: pytorch ImageNet 模型
categories: DeepLearning
description: 因为自己设计了新的网络结构，之前在ImageNet上预训练的模型用不上了，如果不使用预训练模型直接在现有特定任务数据集上进行训练，效果不是很好，所以打算试试先在ImageNet上训练预训练模型，然后在现有特定任务数据集上做微调，这里记录了训练的整个流程。like a [link](https://code-conquer.github.io).
---

# ImageNet数据集下载及预处理

数据集选择常用的`ISLVRC2012` （ImageNet Large Scale Visual Recognition Challenge）

* 训练集<a href=" http://www.image-net.org/challenges/LSVRC/2012/nnoupb/ILSVRC2012_img_train.tar"> http://www.image-net.org/challenges/LSVRC/2012/nnoupb/ILSVRC2012_img_train.tar</a>（138G）
* 测试集 <a href=" http://www.image-net.org/challenges/LSVRC/2012/nnoupb/ILSVRC2012_img_test.tar ">http://www.image-net.org/challenges/LSVRC/2012/nnoupb/ILSVRC2012_img_test.tar </a>（12.7G）
* 验证集<a href="http://www.image-net.org/challenges/LSVRC/2012/nnoupb/ILSVRC2012_img_val.tar ">http://www.image-net.org/challenges/LSVRC/2012/nnoupb/ILSVRC2012_img_val.tar </a> （6.3G）



## 预处理

为了使用Pytorch自带的DataLoader函数进行数据集加载，我们需要将每一个相同类的图片放到相同的文件夹。

_训练集只需要解压即可_:

```
mkdir train && mv ILSVRC2012_img_train.tar train/ && cd train
tar -xvf ILSVRC2012_img_train.tar && rm -f ILSVRC2012_img_train.tar
find . -name "*.tar" | while read NAME ; do mkdir -p "${NAME%.tar}"; tar -xvf "${NAME}" -C "${NAME%.tar}"; rm -f "${NAME}"; done
cd ..
```

__但是验证集图片都在一个文件夹，需要重新分类：__

```
mkdir val && mv ILSVRC2012_img_val.tar val/ && cd val && tar -xvf ILSVRC2012_img_val.tar
wget -qO- https://raw.githubusercontent.com/soumith/imagenetloader.torch/master/valprep.sh | bash
```

之后将训练集和验证集文件夹名称改为 __train__ 、 __val__ 

# 训练模型

## 训练源码的准备

首先去github上找到pytorch的examples，这里面有很多的代码， __Training Imagenet Classifiers with Residual Networks__   里面的代码就是我们想要使用的。

主要修改的地方就是 __创建模型实例时，使用自己的模型创建__  就ok啦。

在命令行内输入以下命令就可以训练啦：

```
python main.py -a resnet101 --dist url 'tcp://127.0.0.1:8001' --dist-backend 'nccl' --world-size 1 --rank 0 /data/dataset/imagenet 
```

__注意__ ：有一些参数要根据自己的需要作出修改，这里给出的是我所训练时的命令。