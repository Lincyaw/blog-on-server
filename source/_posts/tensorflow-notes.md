---
title: tensorflow notes
date: 2019-08-15 17:51:51
tags: [Tensorflow,AI]
---
像TensorFlow这样的编程框架不仅仅可以缩短你的开发时间，而且还可以使你的程序运行得更高效更快。因为这些框架都是经过精心设计和高效实现的。所以我是强烈建议大家在实际的商业项目中使用编程框架的。

在python中使用tensorflow就像使用numpy库一样，首先要将其导入。导入matplotlib库时可能会出现“No moudle named 'matplotlib'”，解决方法是在anaconda prompt中输入activate tensorflow来激活我们前一篇文章中创建的tensorflow环境，然后再输入pip install matplotlib来安装matplotlib库。以后出现类似找不到库的错误提示都可以用这种方法来解决。

```
import math
import numpy as np
import h5py
import matplotlib.pyplot as plt
import tensorflow as tf
from tensorflow.python.framework import ops
from tf_utils import load_dataset, random_mini_batches, convert_to_one_hot, predict
np.random.seed(1)
```
首先向大家展示用tensorflow来定义下面的函数。
𝑙𝑜𝑠𝑠=(𝑦̂ ,𝑦)=(𝑦̂ (𝑖)−𝑦(𝑖))2(1)
```
y_hat = tf.constant(36, name='y_hat')            # 定义一个tensorflow常量
y = tf.constant(39, name='y')                   

loss = tf.Variable((y - y_hat)**2, name='loss')  # 定义一个tensorflow变量，这个变量就表示了上面的loss函数

init = tf.global_variables_initializer() # 这个可以看作是tensorflow的固定写法，后面会使用init来初始化loss变量                                                 
with tf.Session() as session:                    # 创建一个tensorflow的session
    session.run(init)                            # 用这个session来执行init初始化操作
    print(session.run(loss))                     # 用session来执行loss操作，并将loss的值打印处理
	
```