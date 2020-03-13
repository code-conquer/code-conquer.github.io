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

__下载地址__

* 训练集 http://www.image-net.org/challenges/LSVRC/2012/nnoupb/ILSVRC2012_img_train.tar（138G）
* 测试集 http://www.image-net.org/challenges/LSVRC/2012/nnoupb/ILSVRC2012_img_test.tar （12.7G）
* 验证集http://www.image-net.org/challenges/LSVRC/2012/nnoupb/ILSVRC2012_img_val.tar （6.3G）



__预处理__

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

暂时更新数据集这里，后面找时间再更。