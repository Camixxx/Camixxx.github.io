---
title: Matlab问题整理-1
categories:
- Math
tags:
- Matlab
date: 2017-11-01 13:30:01
---

前两天在替人写作的时候遇到了一些matlab问题，整理在博客中，涉及到一些计算方法。

## 生成三角矩阵

以3*3的三角矩阵为例：

``` matlab
  tril(ones(3,3),0)   %下三角矩阵
  triu(ones(3,3),0)   %上三角矩阵
```

但是当矩阵很大时，会出现以下问题：

``` matlab
>> n=10^6
n =  1000000
>> triu(ones(n,n),0)
error: out of memory or dimension too large for Octave's index type
```
我是在octave上写的，在matlab中报错信息可能不同。但我在公式中所要计算的其实是这个下三角矩阵的逆，直接求出矩阵的逆就可以了，所以就利用了matlab中的稀疏矩阵。
<!--more-->
首先写一个下三角矩阵

``` matlab
>> n=3;A =tril(ones(n,n),0)
A =
   1   0   0
   1   1   0
   1   1   1
```

而一个3*3的下三角矩阵A的逆如下，是一个对角矩阵加对角矩阵下面的那个值刚好为-1，成一条带状。

``` matlab
>> inv(A)
ans =
   1   0   0
  -1   1   0
  -0  -1   1
```

所以利用稀疏矩阵的写法，当我要写一个 n =10^6 的下三角阵的逆：

``` matlab
e = ones(n,1);
Dinv = spdiags([-e e 0*e], [-1 0 1], n, n);
```

### 稀疏矩阵的写法：

    spdiags函数：Extract and create sparse band and diagonal matrices

这个函数可以生成对角矩阵和带状稀疏矩阵，有四个参数。

     B = spdiags(A)

提取矩阵A(大小为m×n)的所有非零对角列。B的大小为 min(m,n)×p，其中p表示A的p个非零对角列

     [B,d] = spdiags(A）  

同上，这里d表示一个列向量，对应原来A的非零对角列的的标号

     B = spdiags(A,d)

从矩阵A中取出由D指定的对角线元素，并保存在矩阵B中。

     A = spdiags(B,d,A)
Replaces the diagonals specified by d with the columns of B.
The output is sparse.

     A = spdiags(B,d,m,n)
产生一个m×n稀疏矩阵A，其元素是B中的列元素放在由D指定的对角线位置上。

Roughly, A, B, and d are related by
    ``` matlab
         for k = 1:p
          B(:,k) = diag(A,d(k))
         end
    ```

## Sherman-Morrison formula

${(B+{uv}^{T})}^{-1} = {B}^{-1}-\frac{ {B}^{-1}{uv}^{T}{B}^{-1}}{1+{v}^{T}{B}^{-1}u}$

通过实现代码计算，发现当n极大时，按照左边的方法计算所耗费的时间远远大于右边所耗费的时间。
左式是计算完括号中数据后，进行求逆运算，而右则是先提前计算好B矩阵的逆，再直接求。

在matlab中利用了 tic  toc来测量运算时间
