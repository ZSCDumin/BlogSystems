---
title: HyperOpt调参
date: 2019-03-12 18:37:21
tags: 机器学习
---

# 1. 机器学习调参工具之HyperOpt

## 1.1 示例代码：

```python
from hyperopt import hp, fmin, rand, tpe, space_eval, anneal, partial
```


```python
# 定义目标函数
def q (args) :
    x, y = args
    return x ** 2 + y ** 2
```


```python
# 定义参数空间
space = [hp.uniform('x', 0, 1), hp.normal('y', 0, 1)]
```


```python
# 指定搜索算法
# algo指定搜索算法，目前支持以下算法：
# ①随机搜索(hyperopt.rand.suggest)
# ②模拟退火(hyperopt.anneal.suggest)
# ③TPE算法（hyperopt.tpe.suggest，算法全称为Tree-structured Parzen Estimator Approach）

algo = partial(anneal.suggest,)
```


```python
# 寻找最佳匹配的space,使fn的函数返回值最小
best = fmin(q, space, algo=algo,max_evals=100)
```

    100%|██████████| 100/100 [00:00<00:00, 1026.67it/s, best loss: 7.504195016189939e-06]



```python
print(best)
```

    {'x': 0.002299082182183151, 'y': 0.0014894348377011664}

