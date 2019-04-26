---
title: HyperOptSklearn调参
date: 2019-03-12 18:37:45
tags: 机器学习
---

# 1. 机器学习调参工具之HyperOptSklearn

## 1.1 示例代码：

```python
from hpsklearn import HyperoptEstimator, any_classifier, any_preprocessing
from sklearn.datasets import load_iris
from hyperopt import tpe
import numpy as np
```

    WARN: OMP_NUM_THREADS=None =>
    ... If you are using openblas if you are using openblas set OMP_NUM_THREADS=1 or risk subprocess calls hanging indefinitely



```python
# Download the data and split into training and test sets
iris = load_iris()
X = iris.data
y = iris.target
test_size = int(0.2 * len(y))
np.random.seed(13)
indices = np.random.permutation(len(X))
X_train = X[indices[:-test_size]]
y_train = y[indices[:-test_size]]
X_test = X[indices[-test_size:]]
y_test = y[indices[-test_size:]]
```


```python
# Instantiate a HyperoptEstimator with the search space and number of evaluations
estim = HyperoptEstimator(classifier=any_classifier('my_clf'),
                          preprocessing=any_preprocessing('my_pre'),
                          algo=tpe.suggest,
                          max_evals=100,
                          trial_timeout=120)
```


```python
# Search the hyperparameter space based on the data
estim.fit( X_train, y_train )
```

    100%|██████████| 1/1 [00:00<00:00,  1.59it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  2.03it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  8.80it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  1.28it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  3.07it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  7.68it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00, 12.13it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00, 12.90it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  9.88it/s, best loss: 0.04166666666666663]
      0%|          | 0/1 [00:00<?, ?it/s, best loss: ?]

    /home/hadoop/anaconda3/lib/python3.6/site-packages/sklearn/linear_model/stochastic_gradient.py:117: DeprecationWarning: n_iter parameter is deprecated in 0.19 and will be removed in 0.21. Use max_iter and tol instead.
      DeprecationWarning)
    


    100%|██████████| 1/1 [00:00<00:00, 13.00it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  2.57it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00, 13.18it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00, 12.58it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  9.96it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00, 15.72it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  1.13it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  8.16it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  2.33it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  9.97it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  6.35it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:02<00:00,  2.89s/it, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  9.30it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  5.56it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:02<00:00,  2.29s/it, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  1.43it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  6.32it/s, best loss: 0.04166666666666663]
      0%|          | 0/1 [00:00<?, ?it/s, best loss: ?]

    /home/hadoop/anaconda3/lib/python3.6/site-packages/sklearn/linear_model/stochastic_gradient.py:117: DeprecationWarning: n_iter parameter is deprecated in 0.19 and will be removed in 0.21. Use max_iter and tol instead.
      DeprecationWarning)
    


    100%|██████████| 1/1 [00:00<00:00,  6.31it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:03<00:00,  3.20s/it, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  5.44it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  6.14it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:03<00:00,  3.01s/it, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  2.74it/s, best loss: 0.04166666666666663]
      0%|          | 0/1 [00:00<?, ?it/s, best loss: ?]

    /home/hadoop/anaconda3/lib/python3.6/site-packages/sklearn/linear_model/stochastic_gradient.py:117: DeprecationWarning: n_iter parameter is deprecated in 0.19 and will be removed in 0.21. Use max_iter and tol instead.
      DeprecationWarning)
    


    100%|██████████| 1/1 [00:00<00:00,  8.37it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:03<00:00,  3.17s/it, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:01<00:00,  1.19s/it, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  9.40it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  9.44it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:01<00:00,  1.41s/it, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:01<00:00,  1.89s/it, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  9.26it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  6.86it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  2.03it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:01<00:00,  1.19s/it, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  9.23it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:01<00:00,  1.15s/it, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  6.60it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  2.46it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  8.91it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  4.77it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  9.09it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  5.77it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  1.56it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:01<00:00,  1.10s/it, best loss: 0.04166666666666663]
      0%|          | 0/1 [00:00<?, ?it/s, best loss: ?]

    /home/hadoop/anaconda3/lib/python3.6/site-packages/sklearn/linear_model/stochastic_gradient.py:117: DeprecationWarning: n_iter parameter is deprecated in 0.19 and will be removed in 0.21. Use max_iter and tol instead.
      DeprecationWarning)
    


    100%|██████████| 1/1 [00:00<00:00,  7.84it/s, best loss: 0.04166666666666663]
      0%|          | 0/1 [00:00<?, ?it/s, best loss: ?]

    /home/hadoop/anaconda3/lib/python3.6/site-packages/sklearn/linear_model/stochastic_gradient.py:117: DeprecationWarning: n_iter parameter is deprecated in 0.19 and will be removed in 0.21. Use max_iter and tol instead.
      DeprecationWarning)
    


    100%|██████████| 1/1 [00:00<00:00,  6.07it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  6.03it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  3.08it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  6.88it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  3.65it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  6.19it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:02<00:00,  2.11s/it, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:01<00:00,  1.03s/it, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  2.00it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  4.24it/s, best loss: 0.04166666666666663]
      0%|          | 0/1 [00:00<?, ?it/s, best loss: ?]

    /home/hadoop/anaconda3/lib/python3.6/site-packages/sklearn/linear_model/stochastic_gradient.py:117: DeprecationWarning: n_iter parameter is deprecated in 0.19 and will be removed in 0.21. Use max_iter and tol instead.
      DeprecationWarning)
    


    100%|██████████| 1/1 [00:00<00:00,  8.10it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  6.05it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:02<00:00,  2.37s/it, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  4.22it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:01<00:00,  1.32s/it, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  6.87it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  5.92it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:01<00:00,  1.34s/it, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  1.85it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  4.07it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  5.56it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  9.04it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  6.60it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  8.98it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  8.93it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:01<00:00,  1.00s/it, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  9.08it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  1.30it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  9.02it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  4.11it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  6.58it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  8.87it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  7.09it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  5.95it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  7.00it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:01<00:00,  1.31s/it, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:01<00:00,  1.54s/it, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  1.34it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  1.93it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  3.88it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:01<00:00,  1.48s/it, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:02<00:00,  2.27s/it, best loss: 0.04166666666666663]
      0%|          | 0/1 [00:00<?, ?it/s, best loss: ?]

    /home/hadoop/anaconda3/lib/python3.6/site-packages/sklearn/linear_model/stochastic_gradient.py:117: DeprecationWarning: n_iter parameter is deprecated in 0.19 and will be removed in 0.21. Use max_iter and tol instead.
      DeprecationWarning)
    


    100%|██████████| 1/1 [00:00<00:00,  7.80it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  8.75it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  5.19it/s, best loss: 0.04166666666666663]
    100%|██████████| 1/1 [00:00<00:00,  7.03it/s, best loss: 0.04166666666666663]



```python
# Show the results
print(estim.score(X_test, y_test))
```

    1.0



```python
print( estim.best_model() )
```

    {'learner': ExtraTreesClassifier(bootstrap=False, class_weight=None, criterion='gini',
               max_depth=4, max_features=None, max_leaf_nodes=None,
               min_impurity_decrease=0.0, min_impurity_split=None,
               min_samples_leaf=1, min_samples_split=2,
               min_weight_fraction_leaf=0.0, n_estimators=590, n_jobs=1,
               oob_score=False, random_state=0, verbose=False,
               warm_start=False), 'preprocs': (MinMaxScaler(copy=True, feature_range=(0.0, 1.0)),), 'ex_preprocs': ()}

