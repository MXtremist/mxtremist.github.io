---
layout:  post
title:  算法复习笔记整理
date:  2020-08-05
Author:  MXtremist
categories: 
tags:  [notes, study]

comments:  true

---

算法设计与分析复习笔记，按教学顺序。

<!-- more -->

# 准备知识

## RAM模型

三类操作：简单操作（比较两个元素、在图遍历时对一个节点染色等）；复杂操作（循环和子程序调用）；存储访问（对存储单元的w/r）

计算模型：易用性和精确性

## 算法设计及证明

### 算法问题的规约

输入：明确规定了算法接受的所有合法输入；

输出：明确规定了对于每一个合法的输入值，相应的输出值应该是什么

例如：

输入：任意两个非负整数a、b

输出：a、b的最大公约数

### 算法的证明——数学归纳法

弱归纳&强归纳

## 算法分析

性能指标：关键操作 critical operation

| 算法问题         | 关键操作               |
| ---------------- | ---------------------- |
| 排序、查找、选择 | 元素的比较             |
| 图遍历           | 节点信息的简单处理     |
| 串匹配           | 字符的比较             |
| 矩阵运算         | 两个矩阵元素的简单运算 |

其余的辅助操作通常和关键操作呈线性关系

$D(n):算法输入集合，f(I):对于输入I的时间复杂度，Pr(I):输入I出现的概率$

最坏情况时间复杂度：

$W(n)=\max_{I\in D(n)}f(I)$

平均情况时间复杂度：

$A(n)=\sum_{I\in D(n)}Pr(I)*f(I)$

# 数学基础

## 渐进增长率

### O：上界

#### 定义

- $O(g(n))=\{f(n):{\exist}c>0,n_{0}>0,{\forall}n{\ge}n_{0},0{\le}f(n){\le}cg(n)\}$
- $f(n)=O(g(n))\iff\lim_{n \to \infty}{\frac{f(n)}{g(n)}=c<\infin}$

#### 含义

当n足够大时，f(n)的增长率不会超过g(n)的

或者说，如果一个任务是O(g(n))，其肯定能在c*g(n)时间完成（g(n)足够大，下同）

#### 举例

n是O(n)，logn也是

### o：严格的等级差

#### 定义

- $o(g(n))=\{f(n):{\exist}c>0,n_{0}>0,{\forall}n{\ge}n_{0},0{\le}f(n)<cg(n)\}$
- $f(n)=O(g(n))\iff\lim_{n \to \infty}{\frac{f(n)}{g(n)}=0}$

#### 含义

当n足够大时，f(n)的增长率小于g(n)的，即，总可以通过增加问题的规模使得f(n)和g(n)之间有任意大的差距

或者说，如果一个任务是o(g(n))，其肯定能在少于c*g(n)的时间完成

#### 举例

logn是o(n)

### Ω：下界

#### 定义

- $\Omega(g(n))=\{f(n):{\exist}c>0,n_{0}>0,{\forall}n{\ge}n_{0},f(n){\ge}cg(n)\}$
- $f(n)=\Omega(g(n))\iff\lim_{n \to \infty}{\frac{f(n)}{g(n)}=c>0}$

#### 含义

当n足够大时，f(n)的增长率不会低于g(n)的

或者说，如果一个任务是Ω(g(n))，其至少要用c*g(n)的时间完成

#### 举例

n是O(n)，nlogn也是

### ω：严格的等级差

#### 定义

- $\omega(g(n))=\{f(n):{\exist}c>0,n_{0}>0,{\forall}n{\ge}n_{0},f(n)>cg(n)\}$
- $f(n)=\omega(g(n))\iff\lim_{n \to \infty}{\frac{f(n)}{g(n)}=\infin}$

#### 含义

当n足够大时，f(n)的增长率大于g(n)的，即，总可以通过增加问题的规模使得f(n)和g(n)之间有任意大的差距

或者说，如果一个任务是ω(g(n))，其无法在c*g(n)的时间完成

#### 举例

n是ω(logn)

### Θ：精确描述

#### 定义

- $\Theta(g(n))=\{f(n):{\exist}c_1>0,c_2>0,n_0>0,{\forall}n{\ge}n_0,c_1g(n){\le}f(n){\le}c_2g(n)\}$
- $f(n)=\Theta(g(n))\iff\lim_{n \to \infty}{\frac{f(n)}{g(n)}=c,c\in(0,\infin)}$

#### 含义

f(n)与g(n)处于同一水平

或者说，如果一个任务是Θ(g(n))，其在c*g(n)的时间完成

#### 举例

2n是Θ(n)

### 关于

- o、ω是传递的
- O、Ω是传递、自反的，即n=O(n)
- Θ是等价的，且f=Θ(g) iff f=O(g), f=Ω(g)
- 若f=O(g)，则g=Ω(f)，对于小的也一样

<img src="https://i.loli.net/2020/08/05/MR39kXIYLQvblWG.png" style="zoom:50%;" />

o：1，ω：2，O：1+3，Ω：2+3，Θ：3

## 数学运算背后的算法操作

#### 取整、对数（略）

#### 阶乘

Stirling公式：$n!=\sqrt{2{\pi}n}(\frac{n}{e})^n(1+\Theta(\frac1n))\approx\sqrt{2{\pi}n}(\frac{n}{e})^n$

#### 常见级数求和

多项式级数：$\sum_{i=1}^{n}i=\frac{n(n+1)}2,\sum_{i=1}^{n}i^2=\frac13n(n+\frac12)(n+1),\sum_{i=1}^{n}i^k=\Theta(\frac1{k+1}n^{k+1})$

几何级数：$\sum_{i=1}^{k}r^i=\frac{r^{k+1}-1}{r-1}$

#### 期望E[x]

指标随机变量：

$X_i=I\{事件e_i\}=\left\{\begin{matrix}1,事件发生\\0，事件未发生\end{matrix}\right.$

指标随机变量的期望值就等同于事件发生的概率

期望值的线性特征：

$给定X_1,X_2,...,X_k及其线性函数h(X_1,X_2,...,X_k),则有：$

$E[h(X_1,X_2,...,X_k)]=h(E[X_1],E[X_2],...,E[X_k])$

例如：$E[\sum x_i]=\sum E[x_i]$

## 求解递归方程

#### 替换法

*若函数平滑（即f(2n)=Θ(f(n))），则对于$\left \lceil  \right \rceil,\left \lfloor  \right \rfloor $操作可以忽略

Guess and Prove
$$
e.g.T(n)=2T(n/2)+n \\
Guess:T(n)=O(nlogn)\\
Then\ need\ to\ prove:T(n)\le{cnlogn}\\
根据归纳假设，我们有：T(n/2){\le}cn/2*log(n/2)，所以\\
T(n)=2T(n/2)+n{\le}cnlog(n/2)+n{\le}cnlogn(取c{\ge}2)
$$
需要注意的是，在上述证明中，套用定义只需在某个n~0~后成立即可，上述例子对于T(1)就不成立

#### 递归树

分治递归的形式:$T(n)=aT(n/b)+f(n)$

a：划分为a个子问题；b子问题规模为原先的1/b；f(n)：子问题划分与合并的代价

举例：

<img src="https://i.loli.net/2020/08/06/39KSHIMBLtdVRfi.png"/>

#### Master定理

对于:$T(n)=aT(n/b)+f(n)$，设$E=log_ba$
$$
case\ 1:f(n)=O(n^{E-\epsilon}),\epsilon>0,then\\
T(n)=\Theta(n^E)，公比大于1，等于叶子层\\
case\ 2:f(n)=\Theta(E),then\\
T(n)=\Theta(f(n)logn)，公比等于1，等于层高*每层代价\\
case\ 3:f(n)=\Omega(n^{E+\epsilon}),\epsilon>0,and\ \exist c<1,af(n/b)\le cf(n),then\\
T(n)=\Theta(f(n))，公比小于1，等于根
$$
Master定理并没有涵盖所有情况，例如$T(n)=\sqrt nT(\sqrt n)+n$，可以用替换法进行求解

# 排序

## 线性表，从蛮力到快排



## 堆

## 合并排序

## 基于比较的排序的下界

# 选择

## 期望线性时间选择

## 最坏情况线性时间选择

# 查找

## 折半查找

## 二叉树

## 并查集

# 图遍历

## DFS

## BFS

# 图优化

## 最小生成树算法

## 最短路径

## 贪心

## 动态规划

# 计算复杂性理论初步

## P和NP 归约

## NP完全性的证明



最后修改于2020-8-5