---
title: Apriori算法
date: 2018-08-12 17:34:56
tags: 大数据

---
# Apriori算法解析
![](https://images2015.cnblogs.com/blog/659319/201511/659319-20151128123526249-2019227294.png)

## 参考原文
> [参考博文的文章链接](https://www.cnblogs.com/90zeng/p/apriori.html)

## 参考代码

```python
# -*- coding: utf-8 -*-
"""
Apriori算法测试.
@author: ZSCDumin

"""


def loadDataSet():
    '''
    创建简单的数据集
    '''
    return [[1, 3, 4], [2, 3, 5], [1, 2, 3, 5], [2, 5]]


def createC1(dataSet):
    """
    函数说明：C1 是大小为1的所有候选项集的集合,是不重复的frozenset集合.
    """

    C1 = []
    for transaction in dataSet:
        for item in transaction:
            if not [item] in C1:
                C1.append([item])
    C1.sort()
    return list(map(frozenset, C1))


def scanD(D, Ck, minSupport):
    """
    函数说明：该函数用于从大小为1的所有候选项集的集合C1生成频繁项集列表L1，即retList。
    数据集:D
    候选项集列表:Ck
    最小支持度:minSupport
    返回值： 频繁项集列表：retList
            包含支持度值的字典：supportData
    """
    ssCnt = {}

    for tid in D:
        for can in Ck:
            if can.issubset(tid):
                if not can in ssCnt:
                    ssCnt[can] = 1
                else:
                    ssCnt[can] += 1

    numItems = float(len(D))
    reList = []
    supportData = {}
    for key in ssCnt:
        # 每个项集的支持度
        support = ssCnt[key] / numItems
        # 将满足最小支持度的项集，加入到reList
        if support >= minSupport:
            reList.insert(0, key)

        # 汇总支持度数据
        supportData[key] = support
    return reList, supportData


# Aprior算法
def aprioriGen(Lk, k):
    '''
    由初始候选项集的集合Lk生成新的生成候选项集，
    k表示生成的新项集中所含有的元素个数
    '''
    retList = []
    lenLk = len(Lk)
    for i in range(lenLk):
        for j in range(i + 1, lenLk):
            L1 = list(Lk[i])[: k - 2]
            L2 = list(Lk[j])[: k - 2]
            L1.sort()
            L2.sort()
            if L1 == L2:
                retList.append(Lk[i] | Lk[j])
    return retList


def apriori(dataSet, minSupport=0.5):
    # 构建初始候选项集C1
    C1 = createC1(dataSet)

    # 将dataSet集合化，以满足scanD的格式要求
    D = list(map(set, dataSet))

    # 构建初始的频繁项集，即所有项集只有一个元素
    L1, suppData = scanD(D, C1, minSupport)
    L = [L1]
    # 最初的L1中的每个项集含有一个元素，新生成的
    # 项集应该含有2个元素，所以 k=2
    k = 2

    while (len(L[k - 2]) > 0):
        Ck = aprioriGen(L[k - 2], k)
        Lk, supK = scanD(D, Ck, minSupport)

        # 将新的项集的支持度数据加入原来的总支持度字典中
        suppData.update(supK)

        # 将符合最小支持度要求的项集加入L
        L.append(Lk)

        # 新生成的项集中的元素个数应不断增加
        k += 1
    # 返回所有满足条件的频繁项集的列表，和所有候选项集的支持度信息
    return L, suppData


def calcConf(freqSet, H, supportData, brl, minConf=0.7):
    '''
    计算规则的可信度，返回满足最小可信度的规则。

    freqSet(frozenset):频繁项集
    H(frozenset):频繁项集中所有的元素
    supportData(dic):频繁项集中所有元素的支持度
    brl(tuple):满足可信度条件的关联规则
    minConf(float):最小可信度
    '''
    prunedH = []
    for conseq in H:
        conf = supportData[freqSet] / supportData[freqSet - conseq]
        if conf >= minConf:
            print(freqSet - conseq, '-->', conseq, 'conf:', conf)
            brl.append((freqSet - conseq, conseq, conf))
            prunedH.append(conseq)
    return prunedH


def rulesFromConseq(freqSet, H, supportData, brl, minConf=0.7):
    '''
    对频繁项集中元素超过2的项集进行合并。

    freqSet(frozenset):频繁项集
    H(frozenset):频繁项集中的所有元素，即可以出现在规则右部的元素
    supportData(dict):所有项集的支持度信息
    brl(tuple):生成的规则

    '''
    m = len(H[0])

    # 查看频繁项集是否大到移除大小为 m　的子集
    if len(freqSet) > m + 1:
        Hmp1 = aprioriGen(H, m + 1)
        Hmp1 = calcConf(freqSet, Hmp1, supportData, brl, minConf)

        # 如果不止一条规则满足要求，进一步递归合并
        if len(Hmp1) > 1:
            rulesFromConseq(freqSet, Hmp1, supportData, brl, minConf)


# 生成关联规则
def generateRules(L, supportData, minConf=0.7):
    # 频繁项集列表、包含那些频繁项集支持数据的字典、最小可信度阈值
    bigRuleList = []  # 存储所有的关联规则
    for i in range(1, len(L)):  # 只获取有两个或者更多集合的项目，从1,即第二个元素开始，L[0]是单个元素的
        # 两个及以上的才可能有关联一说，单个元素的项集不存在关联问题
        for freqSet in L[i]:
            H1 = [frozenset([item]) for item in freqSet]
            # 该函数遍历L中的每一个频繁项集并对每个频繁项集创建只包含单个元素集合的列表H1
            if i > 1:
                # 如果频繁项集元素数目超过2,那么会考虑对它做进一步的合并
                rulesFromConseq(freqSet, H1, supportData, bigRuleList, minConf)
            else:  # 第一层时，后件数为1
                calcConf(freqSet, H1, supportData,
                         bigRuleList, minConf)
    return bigRuleList


if __name__ == '__main__':
    # # 导入数据集
    # myDat = loadDataSet()
    # # 选择频繁项集
    # L, suppData = apriori(myDat)
    # # 生成规则
    # rules = generateRules(L, suppData, minConf=0.7)
    # print("规则：", rules)

    # 毒蘑菇案例分析
    mushDataSet = [line.split() for line in open(
        './mushroom.dat').readlines()]

    L, supportData = apriori(mushDataSet, minSupport=0.3)

    for item in L[3]:
        if '2' in item:
            print(item)
```