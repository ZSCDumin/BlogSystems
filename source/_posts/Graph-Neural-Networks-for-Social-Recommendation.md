---
title: Graph Neural Networks for Social Recommendation
date: 2019-03-13 15:16:40
tags: 图神经网络
mathjax: true
---

# Graph Neural Networks for Social Recommendation

## 1. 摘要

- **构建基于图神经网络的推荐系统的三大挑战**
  - the user-item graph encodes both interactions and their associated opinions
  - social relations have heterogeneous strengths
  - users involve in two graphs (e.g., the user-user social graph and the user-item graph)

## 2. 介绍

- **难点**

  - Their main idea is how to iteratively aggregate feature information from local graph neighborhoods using neural networks. Meanwhile, node information can be propagated through a graph after transformation and aggregation.

- **GNN 的作用**
  - Hence, GNNs naturally integrate the node information as well as the topological structure and have been demonstrated to be powerful in representation learning [ 5 , 7 , 15 ]. On the other hand, data in social recommendation can be represented as graph data with two graphs.

## 3. 本文模型

![model](https://ws1.sinaimg.cn/large/006wCagogy1g10b2rj8ulj31dq0ttqdl.jpg)

### 3.1 用户模型

#### 3.1.1 Item Aggregation

> The purpose of item aggregation is to learn item-space user latent factor $h_{i}^{I}$ by considering items a user $u_{i}$ has interacted with and users’ opinions on these items.

$$h^{I}_{i} = σ(W · Aggre_{items} ({x_{ia} ,∀a ∈ C(i)}) + b)$$

- $h^{I}_{i}$: item-space user latent factor
- $C(i)$: item-space user latent factor
- $x_{ia}$: a representation vector to denote opinion-aware interaction between $u_{i}$ and an item $v_{a}$

> The output of MLP is the opinion-aware representation of the interaction between $u_{i}$ and $v_{a}$,$x_{ia}$, as follows:

$$x_{ia} = g_{v}([q_{a}⊕e_{r}])$$

#### 3.1.2 Social Aggregation

> 与 Item Aggregation 做法类似

### 3.2 项目模型

#### 3.2.1 User Aggregation

> 与 Item Aggregation 做法类似

### 3.3 预测评分

> With the latent factors of users and items (i.e., $h_{i}$ and $z_{j}$ ), we can first concatenate them $[h_{i} ⊕ z_{j}]$ and then feed it into MLP for rating prediction as:

$$g_{1} = [h_{i}  ⊕ z_{j}]$$

$$g_{2} = σ(W_{2} · g_{1} + b_{2}) $$

$$g_{l-1} = σ(W_{l} · g_{l-1} + b_{l}) $$

$$r^{′}_{ij} = w^{T} · g_{l−1} $$

- where l is the index of a hidden layer, and $r^{′}_{ij}$ is the predicted rating from $u_{i}$ to $v_{j}$.

### 3.4 模型训练

> **Loss function as follows:**

$$Loss = \frac{1}{2|O|} \sum_{i,j∈O} (r^{′}_{ij} − r_{ij})^{2}$$

- where $|O|$ is the number of observed ratings , and $r_{ij}$ is the ground truth rating assigned by the user i on the item j.

- Optimizer: RMSprop

- Overfitting problem: Dropout

## 4. 实验

### 4.1 数据集

- Ciao
- Epinions

### 4.2 Baselines

- PMF
- SoRec
- SoReg
- SocialMF
- TrustMF
- NeuMF
- DeepSoR
- GCMC+SN

### 4.3 Result

#### 4.3.1 Performance Comparison of Recommender Systems

![1](https://ws1.sinaimg.cn/large/0061Dw64gy1g11961foh9j31890e3n0y.jpg)

#### 4.3.2 Model Analysis

- Effect of Social Network and User Opinions
- Effect of Attention Mechanisms
- Effect of Embedding Size

![2](https://ws1.sinaimg.cn/large/0061Dw64gy1g119615jtbj31d00e8wgt.jpg)
![3](https://ws1.sinaimg.cn/large/0061Dw64gy1g119615b4uj31cl0ehju7.jpg)
![4](https://ws1.sinaimg.cn/large/0061Dw64gy1g1196167voj31c90ek772.jpg)

## 5. 未来工作

- 探索用户和项目之间的更丰富、复杂的属性
- 考虑评分和社交关系的动态性
