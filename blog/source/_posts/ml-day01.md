---
title: 100天机器学习——Day 1
tags:
	- 机器学习	
---
# Day 1 数据预处理
首先安装依赖，这一节里面用到了`numpy`和`pandas`两个库
```shell
pip install numpy
pip install pandas
```
## 第一步 导入库
```python
import numpy as np
import pandas as pd
```

<!-- more -->

## 第二步 导入数据集
```python
dataset = pd.read_csv('Data.csv')
X = dataset.iloc[ : , :-1].values
Y = dataset.iloc[ : , 3].values
```
这里的`iloc`是`pandas`库中选择数据的方式，类似于`python`语法中的**切片**。

## 第三步 处理丢失数据
这里还要用到`sklearn`，所以你还需要安装`sklearn`的依赖
```shell
pip install scipy
pip install scikit-learn
```

```python
from sklearn.preprocessing import Imputer
imputer = Imputer(missing_values = "NaN", strategy = "mean", axis = 0)
imputer = imputer.fit(X[ : , 1:3])
X[ : , 1:3] = imputer.transform(X[ : , 1:3])
```
这里的`Imputer`处理丢失数据的原理是将原来数据集中的`NaN`编程该数据列其他数据的平均值。

## 第四步 解析分类数据
```python
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
labelencoder_X = LabelEncoder()
X[ : , 0] = labelencoder_X.fit_transform(X[ : , 0])
```
**创建虚拟变量**
```python
onehotencoder = OneHotEncoder(categorical_features = [0])
X = onehotencoder.fit_transform(X).toarray()
labelencoder_Y = LabelEncoder()
Y =  labelencoder_Y.fit_transform(Y)
```

## 第五步 拆分数据集为训练集和测试集
```python
from sklearn.model_selection import train_test_split
X_train, X_test, Y_train, Y_test = train_test_split( X , Y , test_size = 0.2, random_state = 0)
```

## 第六步 特征量化
```python
from sklearn.preprocessing import StandardScaler
sc_X = StandardScaler()
X_train = sc_X.fit_transform(X_train)
X_test = sc_X.transform(X_test)
```

[](https://github.com/MLEveryday/100-Days-Of-ML-Code/blob/master/Info-graphs/Day%201.jpg?raw=true)

