[TOC]

## TOPSIS 算法简介

TOPSIS（Technique for Order Preference by Similarity to Ideal Solution）算法又称为逼近理想解排序法、理想点法、理想解法。

​        TOPSIS 算法根据**有限个评价对象与理想化目标的接近程度**进行排序的方法，是在现有的对象中进行相对优劣的评价。理想化目标有两个，一个是最优目标，一个是最劣目标，评价最好的对象应该是与最优目标的距离最近且与最劣目标最远，距离的计算可采用**明考斯基距离**，常用的**欧几里德几何距离**是明考斯基距离的特殊情况。

　　TOPSIS 算法是一种理想目标相似性的顺序选优技术，在多目标决策分析中是一种非常有效的方法。它通过归一化后的数据规范化矩阵，找出多个目标中最优目标和最劣目标（分别用理想解和反理想解表示），分别计算各评价目标与理想解和反理想解的距离，获得各目标与理想解的贴近度，按理想解贴近度的大小排序，以此作为评价目标优劣的依据。贴近度取值在0～1 之间，该值愈接近1，表示相应的评价目标越接近最优水平；反之，该值愈接近 0，表示评价目标越接近最劣水平。

## TOPSIS法的基本原理

　　TOPSIS 算法的基本原理是通过检测评价对象与最优解、最劣解的距离来进行排序，若评价对象最靠近最优解同时又最远离最劣解，则为最好；否则为最差。其中最优解的各指标值都达到各评价指标的最优值。最劣解的各指标值都达到各评价指标的最差值。

　　TOPSIS 算法中“理想解”和“负理想解”是 TOPSIS 算法的两个基本概念。所谓理想解是一设想的最优的解，它的各个属性值都达到各备选方案中的最好的值；而负理想解是一设想的最劣的解，它的各个属性值都达到各备选方案中的最坏的值。

​        方案排序的规则是把各备选方案与理想解和负理想解做比较，若其中有一个方案最接近理想解，而同时又远离负理想解，则该方案是备选方案中最好的方案。

## TOPSIS法的数学模型

### 指标属性同向化

TOPSIS 法使用距离尺度来度量样本差距，使用距离尺度就需要对指标属性进行同向化处理（若一个维度的数据越大越好，另一个维度的数据越小越好，会造成尺度混乱）。通常采用成本型指标向效益型指标转化（即数值越大评价越高，事实上几乎所有的评价方法都需要进行转化），此外，如果需要使用雷达图进行展示，建议此处将所有数据都变成正数。

#### 极小型指标：期望指标值越小越好

$$
\begin{array}{l}
x^{\prime}=\frac{1}{x} \quad(x>0) \\
x^{\prime}=M-x
\end{array}\tag{1}
$$

$M$ 为指标 $x$ 可能取值的最大值。

#### 中间型指标：期望指标值既不要太大也不要太小，适当取中间值最好

$$
x^{\prime}=\left\{\begin{array}{cc}
2 \frac{x-m}{M-m}, & m \leq x \leq \frac{1}{2}(M+m) \\
2 \frac{M-x}{M-m}, & \frac{1}{2}(M+m) \leq x \leq M
\end{array}\right.\tag{2}
$$

$M$ 为指标 $x$ 可能取值的最大值，$m$ 为指标 $x$ 可能取值的最小值。

#### 区间型指标：期望指标的取值最好落在某一个确定的区间最好

$$
x^{\prime}=\left\{\begin{array}{ll}
1-\frac{a-x}{a-a^{*}} & x<a \\
1 & a \leq x \leq b \\
1-\frac{x-b}{b^{*}-b} & x>b
\end{array}\right.\tag{3}
$$

其中 $[a,b]$ 为指标 $x$ 的最佳稳定区间，$[a^*,b^*]$ 为最大容忍区间。

### 建立特征矩阵

​		遇到多目标最优化问题时，通常有 $m$ 个评价目标 $D_1,D_2,...,D_m$，每个目标有 $n$ 个评价指标 $X_1,X_2,...,X_n$。首先使用**专家评估方法**对评价指标进行打分，然后将打分结果表示成矩阵形式，建立下列特征矩阵：
$$
D=\left[
\begin{matrix}
 x_{11}  & \cdots    & x_{1j}      & \cdots & x_{1jn}      \\
 \vdots&& \vdots  & & \vdots\\
 x_{i1}   & \cdots   &  x_{ij}      & \cdots &  x_{in}      \\
 \vdots && \vdots  & & \vdots \\
 x_{m1}   & \cdots   &  x_{mj}      & \cdots &  x_{mn}      \\
\end{matrix}
\right]=\left[
\begin{matrix}
 D_{1}(x_1)       \\
 \vdots \\
 D_{i}(x_j)        \\
 \vdots \\
 D_{m}(x_n)       \\
\end{matrix}
\right]=
\left[
\begin{matrix}
X_1(x_1),...,X_j(x_i),...,X_n(x_m)
\end{matrix}
\right]
$$

### 计算规范化矩阵

​		对特征矩阵进行规范化处理，得到规格化向量 $r_{ij}$，建立关于规格化向量 $r_{ij}$ 的规范化矩阵：
$$
\begin{array}{l}
r_{i j}=\frac{x_{i j}}{\sqrt{\sum_{i=1}^{m} x_{i j}^{2}}} \\
i=1,2, \ldots, m, j=1,2, \ldots, n_{\circ}
\end{array}
$$

### 构造权重规范化矩阵

　　通过计算权重规格化值 $v_{ij}$，建立关于权重规范化值 $v_{ij}$ 的权重规范化矩阵，即每一列元素都除以当前列向量的范数（使用余弦距离度量）：
$$
v_{i j}=w_{j} r_{i j}, i=1,2, \cdots, m, j=1,2, \cdots, n。
$$
​		其中，$w_j$ 是第 $j$ 个指标的权重。常用的权重确定方法有 Delphi 法、对数最小二乘法、层次分析法、熵等。

### 确定理想解和反理想解

　　根据权重规格化值 $v_{ij} $ 来确定理想解 $A^*$ 和反理想解 $A^-$：
$$
\begin{array}{l}
A^{*}=\left(\max _{i} v_{i j} \mid j \in J_{1}\right),\left(\min _{i} v_{i j} \mid j \in J_{2}\right), \mid i=1,2, \cdots, m=v_{1}^{*}, v_{2}^{*}, \cdots, v_{j}^{*}, \cdots, v_{n}^{*} \\
A^{-}=\left(\min _{i} v_{i j} \mid j \in J_{1}\right),\left(\max _{i} v_{i j} \mid j \in J_{2}\right), \mid i=1,2, \cdots, m=v_{1}^{-}, v_{2}^{-}, \cdots, v_{j}^{-}, \cdots, v_{n}^{-}
\end{array}
$$
​		其中 $j_1$ 是收益性指标集，表示在第 $i$ 个指标上的最优值；$j_2$ 是损耗性指标集，表示在第 $i$ 个指标上的最劣值。收益性指标越大，对评估结果越有利；损耗性指标越小，对评估结果越有利。反之，则对评估结果不利。

### 计算距离尺度

　　计算距离尺度，即计算每个目标到理想解和反理想解的距离，距离尺度可以通过 $n$ 维欧几里得距离来计算。目标到理想解 $A^*$ 的距离为 $S^*$，到反理想解 $A^−$ 的距离为 $S^−$：
$$
\begin{array}{l}
S^{*}=\sqrt{\sum_{j=1}^{n}\left(V_{i j}-v_{j}^{*}\right)^{2}} \\
S^{-}=\sqrt{\sum_{j=1}^{n}\left(V_{i j}-v_{j}^{-}\right)^{2}} \\
i=1,2, \cdots, m_{\circ}
\end{array}
$$
​		其中，$v_{j}^{*}$ 与 $v_{j}^{-}$ 分别为第 $j$ 个目标到最优目标及最劣目标的距离，$v_{ij}$ 是第 $i$ 个目标第 $j$ 个评价指标的权重规格化值。$$S^*$$ 为各评价目标与最优目标的接近程度，$$S^*$$ 值越小，评价目标距离理想目标越近，方案越优。

### 计算理想解的贴近度

$$
\begin{array}{l}
C_{i}^{*}=\frac{S_{i}^{-}}{\left(S_{i}^{*}+S_{i}^{-}\right)}, i=1,2, \cdots, m。 \\
0 \leq C_{i}^{*} \leq 1 \text { 当 } C_{i}^{*}=0 \text { 时, } A_{i}=A^{-}
\end{array}
$$

​		式中，$0 \leq C_{i}^{*} \leq 1$。当 $C_{i}^{*}=0$ 时，$A_i=A^-$，表示该目标为最劣目标；当 $C_{i}^{*}= 1$ 时候，$A_i=A^*$，表示该目标为最优目标。在实际的多目标决策中, 最优目标和最劣目标存在的可能性很小。

### 根据理想解的贴近度

​		根据 $C^{*}$ 的值按从小到大的顺序对各评价目标进行排列。排序结果贴近度 $C^{*}$ 值越大，该目标越优，$C^{*}$ 值最大的为最优评标目标。