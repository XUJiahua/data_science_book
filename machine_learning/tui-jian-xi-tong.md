# 推荐系统

## 概述

推荐系统，在整个系统架构中起到的是一个辅助增强的作用。其意义在于，帮助业务系统，留住用户、创造更多流量、提高GMV。比如，今日头条作为一个信息流客户端，就是通过推荐系统一直留着用户看了再看的。

推荐系统解决两类问题：评分预测、TopK预测。评分预测在工业界，是次要问题。所以，主要是TopK预测。

基于互联网上业界大拿的分享，推荐系统不再是简单的协同过滤，而是由**召回**和**排序**两阶段组成。

### 召回

经典的协同过滤在简单推荐系统中，作为直接输出，给到业务层。

在复杂推荐系统中，往往是作为召回的一路。与其他召回策略一样，做生成候选集的工作。候选集与其他召回生成的候选集一起，将经过排序模型，进行重排序，最终给到业务层。

常见的召回策略有：

1. 基于 topic（tag）的召回、实体的召回、地域的召回
2. CF（协同过滤）的召回
3. NN 产生的 embedding 召回等等
4. 人工推荐
5. 热榜（基于计数）

### 排序

为什么需要排序：

1. 召回可有多路，有协同过滤、人工推荐、热榜等。不同召回的排序策略是不一样，合并后并不方便重排序。
2. 加入上下文信息（时间、操作系统等因素），user的特征，item的特征。

排序使用的策略是点击率预估。完成点击率预估的算法有很多，后面介绍。

结合自己的经验、业界的经验，整理本文。

## 历史

评分预测。

TopK排序。

## 算法

### Collaborative Filtering 协同过滤

协同过滤，只使用ID（用户ID、商品ID），不使用其他属性的推荐算法。简单。

#### memory based: user-based

#### memory based: item-based

#### model based: matrix factorization

矩阵分解有两种实现方式，SGD（随机梯度下降），ALS（交替最小二乘）



#### 开源库

选用开源库，性能考量是一个重要方面，能利用CPU多核，利用GPU的优先。

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x5F00;&#x6E90;&#x5E93;&#x540D;&#x79F0;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
      <th style="text-align:left">&#x94FE;&#x63A5;</th>
      <th style="text-align:left">&#x5206;&#x7C7B;</th>
      <th style="text-align:left">&#x4F18;&#x70B9;</th>
      <th style="text-align:left">&#x7F3A;&#x70B9;</th>
      <th style="text-align:left">&#x8BED;&#x8A00;</th>
      <th style="text-align:left">&#x5907;&#x6CE8;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">quora qmf</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">https://github.com/quora/qmf</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">C++</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Implicit</td>
      <td style="text-align:left">Fast Python Collaborative Filtering for Implicit Datasets.</td>
      <td style="text-align:left">https://github.com/benfred/implicit</td>
      <td style="text-align:left">Model-Based CF Item-Based CF</td>
      <td style="text-align:left">&#x5355;&#x673A;&#x591A;&#x6838;&#x3002;GPU&#x652F;&#x6301;&#x3002;</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left">C++/Python</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Spark Mllib</td>
      <td style="text-align:left">
        <p>MLlib is Apache Spark&apos;s scalable machine learning library.</p>
        <p></p>
      </td>
      <td style="text-align:left">https://spark.apache.org/mllib/</td>
      <td style="text-align:left">Model-Based CF</td>
      <td style="text-align:left">&#x5206;&#x5E03;&#x5F0F;&#xFF0C;&#x80FD;&#x5229;&#x7528;&#x591A;&#x6838;&#x591A;&#x673A;&#x3002;</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left">Python/Scala</td>
        <td style="text-align:left">
          <p>&#x4F7F;&#x7528;ALS&#x7B97;&#x6CD5;&#xFF0C;&#x652F;&#x6301;Implicit Feedback</p>
          <p>&#x5EFA;&#x8BAE;&#x751F;&#x4EA7;&#x4F7F;&#x7528;</p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>### Association Rules 关联规则 购物篮分析



排序阶段LR，LR+GBDT，FM，wide and deep，deepFM

### Factorization Machine

没有用户、物品特征就退化为了Matrix Factorization。

## 工程

### 数据库

HBase 作为海量数据的列式存储数据库，有一个明显缺点就是复杂查询性能差，因此一般适合数据查询量大，但查询简单的场景，比如推荐系统当中的已读已推等等场景。

### 监控



