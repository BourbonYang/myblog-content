---
title: "Gram-Schmidt Process and QR Decomposition"
description: "（略）"
date: "2026-10-22"
---

# Gram-Schmidt 处理

Gram-Schmidt处理可以把一组线性无关的（能张成空间的）基，转换成一组正交基。

处理的具体步骤为，对于 $\{\bm{x_1}, \bm{x_2}, \ldots, \bm{x_p}\}$，按以下步骤处理：

$$
\begin{aligned}
\bm{v_1} &= \bm{x_1} \\
\bm{v_2} &= \bm{x_2} - \frac{\bm{x_2} \cdot \bm{v_1}}{\bm{v_1} \cdot \bm{v_1}} \bm{v_1} \\
\bm{v_3} &= \bm{x_3} - \frac{\bm{x_3} \cdot \bm{v_1}}{\bm{v_1} \cdot \bm{v_1}} \bm{v_1} - \frac{\bm{x_3} \cdot \bm{v_2}}{\bm{v_2} \cdot \bm{v_2}} \bm{v_2} \\
& \ \ \vdots \\
\bm{v_p} &= \bm{x_p} - \frac{\bm{x_p} \cdot \bm{v_1}}{\bm{v_1} \cdot \bm{v_1}} \bm{v_1} - \dots -\frac{\bm{x_p} \cdot \bm{v_{p-1}}}{\bm{v_{p-1}} \cdot \bm{v_{p-1}}} \bm{v_{p-1}}
\end{aligned}
$$

得到的 $\{\bm{v_1}, \bm{v_2}, \ldots, \bm{v_p}\}$ 就是一个正交集合。

## 原理

一个向量 $\bm{u}$ 减去其在另一个向量 $\bm{v}$ 上的投影向量 $\bm{\hat{u}}$ 之后，得到的就是 $\bm{u}$ 在垂直于向量 $\bm{v}$ 方向上的分量。

一个新的垂直（正交）的方向，本质上就是一个新的维度。

用一个向量 $\bm{x_p}$ 不断减去它在前 $p-1$ 个向量上的投影，本质上就是在从 $\bm{x_p}$ 中抽出一个、垂直于前 $p-1$ 个向量所张成的空间的方向。

所以在 Gram-Schemidt 处理中，我们以原集合的第一个向量 $\bm{x_1}$ 为基本方向（也就是 $\bm{v_1}$），然后不断把其他向量中的独立方向提取出来，从而得到一个正交基的集合。


# QR分解

一个可逆矩阵 $\mathbf{A}$ 可以表示为一个标准正交基矩阵 $\mathbf{Q}$ 和一个上三角矩阵 $\mathbf{R}$ 的积。

矩阵 $\mathbf{Q}$ 可以通过对矩阵 $\mathbf{A}$ 进行 Gram-Schemidt 处理来得到。矩阵 $\mathbf{R}$ 则可以通过下式得到：

$$
\mathbf{R} = \mathbf{Q^T} \mathbf{A}
$$

## 为什么可以这样算出 R？

$\mathbf{Q}$ 是一个标准正交矩阵，每个列向量的模长都是1，而一个向量关于自身的点积，就是它模长的平方。因此 $\mathbf{Q Q^T}$ 的值正好是一个单位矩阵，也就是说对于矩阵 $\mathbf{Q}$，它的转置矩阵和逆矩阵是同一个矩阵。

所以从 $\mathbf{A} = \mathbf{Q} \mathbf{R}$ 入手，可以给等号左右两边同时在左侧乘以 $\mathbf{Q^T}$ 来消掉 $\mathbf{Q}$，继而得到 $\mathbf{R} = \mathbf{Q^T} \mathbf{A}$ 。

## QR分解的原理

标准正交矩阵 $\mathbf{Q}$ 其实提供了一个新的基底，而上三角矩阵 $\mathbf{R}$ 提供的是、通过新基底来表示原矩阵 $\mathbf{A}$ 所需要的变换。

值得注意的点是，$\mathbf{R}$ 为什么刚好是一个上三角矩阵。

需要让目光回到构建标准正交矩阵 $\mathbf{Q}$ 时的 Gram-Schmidt 处理上， $\bm{v_2} = \bm{x_2} - \frac{\bm{x_2} \cdot \bm{v_1}}{\bm{v_1} \cdot \bm{v_1}} \bm{v_1}$，而 $\bm{x_1} = \bm{v_1}$ ，所以要表示原来的 $\bm{x_2}$，只需要用向量 $\bm{v_1}$ 和 $\bm{v_2}$ 就能做到，不需要用到后面的其他基向量。

“后面的”基向量对表示当前向量没有贡献，因此变换矩阵的对角线以下的元素就都是0。
