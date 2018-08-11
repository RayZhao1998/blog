---
title: 什么是神经网络
tags:
    - 机器学习
    - 深度学习
---



### 什么是神经网络

#### 示例1-单节点神经网络

房价预测问题,这是一个线性回归问题,因为这个函数的输出结果是连续的值.

因为房价永远不可能是负数,所以我们创建了一种叫做**线性整流函数(ReLU)**

![](http://rayzhao98.top/img/house-price-prediction.png)

<!-- more -->
- 输入是房子的大小(x)
- 输出是价格(y)
- 神经元就是这个线性整流函数

![neuron-description](http://rayzhao98.top/img/neuron-description.png)

#### 示例2-多节点神经网络

房价受多种因素影响,如大小,房间数,邮编以及地区的富裕程度.神经网络在其中就扮演了预测房价并自动生成隐藏单元(hidden units).我们只需要给出输入和输出即可.

![](http://rayzhao98.top/img/multiple-house-price-prediction.png)

### 神经网络中的监督学习

在监督学习中,我们给出了数据集并且知道了正确的输出结果,并且知道中间一定有某些联系.

监督学习问题可以分成两类 **回归**和**分类**.

- 在回归问题中,我们在连续的输出结果中预测结果,意味着试图找到一个连续的函数.
- 在分类问题中,我们在离散的结果中预测结果.换句话说,我们试图把输入变量分成不同的离散的类别.

这里有一些监督学习的例子

![](http://rayzhao98.top/img/examples-for-supervised-learning.png)

神经网络有多种,比如**卷积神经网络(Convolution Neural Network 简记为 CNN)**和**循环神经网络(Recurrent Neural Network 简记为 RNN)**

CNN经常用于图片分类,而RNN经常用于一堆时序数据的场景比如翻译.

还有像自动驾驶这样的复杂问题,就需要混合的神经网络结构才能解决.

#### 结构化数据 vs 非结构化数据

结构化数据指的是清晰定义的变量,如价格,年龄等等;而非结构化数据指的是像像素、声音、文本等等.

![](http://rayzhao98.top/img/structure-and-unstructured-data.png)

### 为什么深度学习最近很火

由于社会的数据化,更快的激素那能力和神经网络算法的进化,使得我们能接触到大量的数据使得深度学习变得火起来.

![](http://rayzhao98.top/img/scale-drives-deep-learning-progress.png)

为了追求高性能,要考虑两件事

1. 能够训练一个足够大的神经网络
2. 大量标记过的数据

训练神经网络是一个循环的过程

![](http://rayzhao98.top/img/interative-process-of-nn.png)

需要大量的时间去训练神经网络,这影响到了你的生产力.高速的运算能力帮助我们改进新的算法.
