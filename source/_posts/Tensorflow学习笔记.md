---
title: Tensorflow学习笔记
date: 2019-02-20 17:20:42
tags: Tensorflow
---

# Tensorflow 学习笔记


## 1. 设置tensorflow输出日志级别

```python
import os
os.environ["TF_CPP_MIN_LOG_LEVEL"] = "2"
```

## 2. tf.argmax()函数
```python
A = [[1, 3, 4, 5, 6]]
B = [[1, 3, 4], [2, 4, 1]]

# tf.argmax(y_, 1) 取的是行的最大值对应的下标的索引
# tf.argmax(y_, 0) 取的是列的最大值对应的下标的索引
with tf.Session() as sess:
    print(sess.run(tf.argmax(A, 1)))
    print(sess.run(tf.argmax(B, 0)))
```
运行结果：
```
[4]
[1 1 0]
```
## 3. tf.reduce_mean() 函数
- 函数用于计算张量tensor沿着指定的数轴（tensor的某一维度）上的的平均值，主要用作降维或者计算tensor（图像）的平均值。

```python
reduce_mean(input_tensor,
                axis=None,
                keep_dims=False,
                name=None,
                reduction_indices=None)
```

- 第一个参数input_tensor： 输入的待降维的tensor;
- 第二个参数axis： 指定的轴，如果不指定，则计算所有元素的均值;
- 第三个参数keep_dims：是否降维度，设置为True，输出的结果保持输入tensor的形状，设置为False，输出结果会降低维度;
- 第四个参数name： 操作的名称;
- 第五个参数 reduction_indices：在以前版本中用来指定轴，已弃用;

## 4. 滑动平均-ExponentialMovingAverage()
- 神经网络的优化函数

```python
tf.train.ExponentialMovingAverage(MOVING_AVERAGE_DECAY, global_step)
```

## 5. variables_to_restore()函数

> 是TensorFlow为滑动平均值提供。之前，也介绍过通过使用滑动平均值可以让神经网络模型更加的健壮。我们也知道，其实在TensorFlow中，变量的滑动平均值都是由影子变量所维护的，如果你想要获取变量的滑动平均值需要获取的是影子变量而不是变量本身。

```python
variable_averages = tf.train.ExponentialMovingAverage(mnist_train.MOVING_AVERAGE_DECAY)
variables_to_restore = variable_averages.variables_to_restore()
```