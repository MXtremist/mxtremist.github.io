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

#### 朴素排序

选择排序、冒泡排序

O(n^2^)

##### 插入排序

每次取未处理的元素，在已处理的元素中排序

O(n^2^)

#### 分治排序

##### 快速排序

难分易和

```python
def QuickSort(left,right):
    if left<right:
    	middle=Partition(left,right)
    	QuickSort(left,middle-1)
    	QuickSort(middle,right)
    
def Partition(left,right):
    pivot=A[left]#取基准元素
    pivot_pos=left#基准元素的指针
    for i in range(left+1,right+1):#from left+1 to right
        if A[i]<pivot:
            A[i],A[pivot_pos]=A[pivot_pos],A[i]#小的换到左边
            pivot_pos+=1#发现一个小的，指针右移
    A[left],A[pivot_pos]=A[pivot_pos],A[left]#完成交换，将基准元素放在正确的位置
    return pivot_pos
```

在一次Partition中，数组A在[left,right]范围内，比pivot小的都移到了左边，故结束后pivot已处于数组中的正确位置，即左边都比其小、右边都比其大

分析：

最坏情况下（严格升序/降序），每次比较n且仅规模减小1，故为O(n^2^)

平均情况下

递归方程分析
$$
划分情况等可能出现，即\\
A(n)=O(n)(Partition的代价)+{\frac1n}\sum_{i=0}^{n-1}[A(i)+A(n-1-i)]\\
=O(n)+{\frac2n}\sum_{i=0}^{n-1}A(n)\\
用错项相减，可以算出A(n)=O(nlogn)
$$
指标随机变量分析

根据之前的知识，设元素从a~0~到a~n~，定义指标随机变量$X_{ij}=I\{a_i和a_j发生了比较\}$

则快速排序的代价为$X=\sum_{i=1}^{n-1}\sum_{j=i+1}^{n}X_{ij}$

而**平均情况时间复杂度为上述代价的期望值**，即：

$E[x]=E[\sum_{i=1}^{n-1}\sum_{j=i+1}^{n}X_{ij}]=\sum_{i=1}^{n-1}\sum_{j=i+1}^{n}E[X_{ij}]=\sum_{i=1}^{n-1}\sum_{j=i+1}^{n}Pr\{a_i和a_j发生了比较\}$

将元素分为$a_0...a_{i-1},\ a_i,\ a_{i+1}...a_{j-1},\ a_j,\ a_{j+1}...a_n$五个部分，考虑当前基准元素处于哪个部分

部分①⑤：a~i~和a~j~是否发生比较取决于后续选择，即本次中未比较，可以不做考虑

部分③，a~i~和a~j~将分开到两个数组，永远不会比较

部分②④，选择其中一个作为基准元素，则其发生且仅发生一次比较

故发生比较的概率为 $\frac2{j-i+1}$

带入之前的式子，可以计算出时间复杂度为O(nlogn)

##### 合并排序

易分难和

分而治之：先分为两部分，其在递归过程中已经排序完成，再将已经排好序的两部分合并

```python
def MergeSort(left,right):
    if left<right:
        middle=(left+right)/2
        MergeSort(left,middle)
        MergeSort(middle+1,right)
        Merge(left,middle,right)
        
def Merge(left,middle,right):
    L=A[left:middle]
    R=A[middle+1:right+1]
    i=0,j=0
    for k in range(left,right+1):#重新排列数组A[left:right+1]
        if L[i]<R[j]:	#更小的放在k上
            A[k]=L[i]
            i+=1
        else:
            A[k]=R[j]
            j+=1
```

合并排序是典型的分治算法，其最坏情况时间复杂度为：

$W(n)=2W(n/2)+O(n)$

由Master定理，为O(nlogn)，因此平均情况也为O(nlogn)（下界）

## 堆

### 定义

- 结构特性：完全二叉树
- 偏序特性：父大于子（or小于）

### 维护

#### 修复

当堆顶元素被取走时修复

- 结构修复：将最后一个元素放到堆顶
- 偏序修复：自顶向下，若父最大或到底终止，否则与最大的那个交换，继续向下

由于层高为O(logn)，每次修复操作为O(1)，故复杂度为O(logn)

#### 插入

与修复类似

- 结构：放在最后
- 偏序：自底向上，若父最大或到根终止
- 同样为O(logn)

#### 构建

方法1：执行n次插入，O(nlogn)

方法2：递归，将每个子树整理成堆，然后执行一次修复（不删除元素）

最坏情况时间复杂度 $W(n)=2W(n/2)+O(logn)$，由Master定理，为O(n)

### 应用

假设具有如下堆函数：

```python
def ConstructHeap(A,size)#将数组A整理成堆
def FixHeap_TopDown(A,pos,size)#从pos开始自顶向下执行堆修复
def FixHeap_DownTop(A,pos,size)#从pos开始自底向上执行堆修复
```

#### 堆排序

```python
def HeapSort(A,n):
    size=n
    ConstructHeap(A,size)
    for i in range(n-1,1,-1):#从n-1到1
        A[0],A[i]=A[i],A[0]#当前最大的元素被放在了当前的最后
        size-=1
        FixHeap_TopDown(A,0,size)
```

易得最坏情况下时间复杂度为O(nlogn)

#### 优先队列

优先队列有如下接口：

GET_MAX(A) 返回优先级最高的元素

```python
if len(A) is 0:
    return error
return A[0]
```

EXTRACT_MAX(A) 返回优先级最高的元素，将其从队列中剔除

```python
if len(A) is 0:
    return error
max=A[0]
A[0]=A[len(A)-1]
del A[len(A)-1]
FixHeap_TopDown(A,0,len(A))
return max
```

INSERT(A, key) 添加新元素

```python
A+=key
FixHeap_DownTop(A,len(A)-1,len(A))
```

INCREASE_KEY(A, i, key) 改变指定元素优先级

```python
A[i]=key
FixHeap_DownTop(A,i,len(A))
```

## 基于比较的排序的下界

### 决策树

2-tree（子节点0或2），子节点0个的称为外部节点，2个的称为内部节点

在决策树中，内部节点表示的是（在父节点的比较之后）继续进行的新一轮比较，外部节点表示某一种排序结果，因此，h为走到某一次结果的代价，即某一次的时间复杂度

> 引理1 假设二叉树树高h，叶节点个数L，则L≤2^h^
>
> 定义：EPL 外部路径长度：根节点到所有叶节点路径长度之和
>
> $EPL(T)=0，只有根节点；EPL(T)=EPL(T_L)+EPL(T_R)+N_L+N_R，其中N_L和N_R为左右子树的叶节点个数$
>
> 引理2 越平衡的2-tree，EPL越少

最坏情况时间复杂度的下界：对于n个节点，排序的结果一共有n!种，故决策树的叶节点至少有n!个，由引理1：

$n!\le L\le 2^h$

$h\ge log(n!)=\Omega(nlogn)$，即为下界

平均情况时间复杂度的下界：平均情况下的时间复杂度应该为$\frac{EPL}{L}$，由引理2，保证2-tree尽量平衡，则树高为$\Theta(L)$，EPL为$\Theta(LlogL)$，故对于任一相同节点的2-tree其EPL为$\Omega(L)$，则：
$A(n)=\frac{EPL}{L}=\Omega(\frac{LlogL}{L})=\Omega(logL)=\Omega(log(n!))=\Omega(nlogn)$

# 选择

## 期望线性时间选择

在快速排序中，我们使用了Partition算法，该算法将基准元素移到了恰当的位置，代价为O(n)，利用这个算法，我们可以得到：

```python
def SelectElinear(left, right, k):#k:选择阶为k的数
    if left == right:
        return A[left]
    m=Partition(left,right)#基准元素下标
    x=m-left+1#在当前范围内，左边部分元素个数（包括自己）
    if k==x:
        return A[m]
    elif k>x:#左边部分小于x个，在右边
        return SelectElinear(m+1,right,k-x)
    else:#左边部分大于x个，在左边
        return SelectElinear(left,m-1,k)
```

虽然在最坏情况下为O(n^2^)，但是在平均情况下，计算$A(n)=E[T(n)]的一个上界$

定义指标随机变量$X_k=I\{小于等于基准元素的元素个数为k\}$，由于概率相等，易得$E[X_k]=\frac1n$

$T(n)\le \sum_{k=1}^{n}X_k*(T(max(k-1,n-k))+O(n))\\\ \ \ \ \ \ \ \ =\sum_{k=1}^{n}X_k*T(max(k-1,n-k))+O(n)$

每个子项的含义是在有k个小于或等于基准元素的个数的情况下所需的代价的上界

对其取期望，则有
$$
E[T(n)]\le E[\sum_{k=1}^{n}X_k*T(max(k-1,n-k))+O(n)]\\
=\sum_{k=1}^{n}E[X_k*T(max(k-1,n-k))]+O(n)\\
=\sum_{k=1}^{n}E[X_k]E[T(max(k-1,n-k))]+O(n)\\
=\frac1n\sum_{k=1}^{n}E[T(max(k-1,n-k))]+O(n)
$$
根据max函数的对称性，可以将其简化为

$E[T(n)]\le \frac2n\sum_{k=\frac n2}^{n-1}E[T(k)]+O(n)$

之后，用替换法可以证明其为O(n)
$$
假设O(n)=an，下面证明E[T(n)]\le cn\\
E[T(n)]\le\frac2n\sum_{k=\frac n2}^{n-1}ck+O(n)\\
=\frac{2c}n(\sum_{1}^{n-1}k-\sum_{1}^{\frac n2-1}k)+an\\
=\frac{c}n((n-1)n-(\frac n2-1)\frac n2)+an\\
\le cn-(\frac{cn}4-\frac c2-an)
$$
只需要$\frac{cn}4-\frac c2-an\ge0$即可，即$n\ge \frac{2c}{c-4a}$



## 最坏情况线性时间选择

降低最坏情况下时间复杂度需要的是控制划分的平衡性

方法：

1. 每五个数分为一组，进行一次划分，使得中位数位于中间
2. 用所有小组中位数的中位数m*进行划分
3. 之后的步骤与原算法类似

<img src="https://i.loli.net/2020/08/07/yumwfYViTDLgZvz.png"/>

如上图，所有元素被m\*划分为A、B、C、D四部分，其中B必然比m\*大，C必然比其小，因此在一定程度上保证其平衡性。在最坏情况下，A、D元素也均比m\*小，每次都要递归地到A、C、D三者中找，故其复杂度为：

$W(n)\le W(\frac n5)+W((\frac n{10})*5+(\frac n{10}-1)*2+3)+O(n)=W(\frac n5)+W(\frac7{10}n+6)+O(n)$

可以证明其为O(n)

# 查找

## 折半查找

### 查找算法

二分法

```python
def BinarySearch(A, left, right, key):
    if right<left:
        return -1
    mid=(left+right)/2
    if key == A[mid]:
        return mid
    elif key < A[mid]:
        return BinarySearch(A, left, mid-1, key)
    else:
        return BinarySearch(A, mid+1, right, key)
```

每次都缩小一半，故最坏情况O(logn)

要求：数组有序

### 折半查找的推广

#### 查找峰值

有些数据具有单峰特性，可以利用折半查找

#### 计算$\sqrt n$

折半查找，将中间值的平方和n对比

## 平衡二叉搜索树

### 二叉搜索树

对于树中任意节点，左子树均比它小，右子树均比它大

### 红黑树

#### 定义

##### 一些概念

- 颜色：红/黑
- 2-tree结构
- 外部节点：除非根是外部节点，否则外部节点不含有数据
- 黑色深度：根的黑色深度为0，其他节点的黑色深度为根到该节点的路径上黑色节点的个数（不包括根）

##### 直接定义

- 根节点为黑色，外部节点为黑色
- 红色节点不连续出现
- 在任意节点为根的子树中，所有外部节点的黑色深度相同，将其称为这棵树的黑色高度

##### 递归定义

> ARB 准红黑树：根节点为红色，其余特征满足红黑树

- 唯一一个外部节点（同时为根节点）构成红黑树RB~0~
- 对于h≥1，ARB~h~：根节点红色，左右子树均为RB~h-1~
- 对于h≥1，RB~h~：根节点黑色，左右子树分别为一棵RB~h-1~或ARB~h-1~

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



最后修改于2020-8-7