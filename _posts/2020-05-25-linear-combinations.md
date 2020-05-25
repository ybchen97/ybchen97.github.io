---
layout: post
title: "Linear Combinations"
author: "Yuan Bo Chen"
categories: notes
tags: [linear algebra, math]
---

This article talks about the different ways to look at matrix multiplications through the perspective of linear
combinations.

<br>

## Linear Combination of Columns

$$ 
\mathbf{Ax} = \mathbf{b} \\
$$

This equation is seen as a **linear combination** of **columns** of A. This is an important perspective in linear
algebra. For example, the following equation:

$$
\begin{bmatrix}
	1 & 2 \\
	1 & 0 \\
\end{bmatrix}
\begin{bmatrix}
	x_1 \\
	x_2 \\
\end{bmatrix}
=
\begin{bmatrix}
	3 \\
	1 \\
\end{bmatrix}
$$

can be equally seen as:

$$
x_1
\begin{bmatrix}
	1 \\
	1 \\
\end{bmatrix}
+
x_2
\begin{bmatrix}
	2 \\
	0 \\
\end{bmatrix}
=
\begin{bmatrix}
	3 \\
	1 \\
\end{bmatrix}
$$

Essentially, how many of the first column added with how many of the second column gives us the answer \$\begin{bmatrix}
3 \\\\ 1 \end{bmatrix}\$? Or simply put, which **linear combination** of the first and second column of \$\mathbf{A}\$
yields us the resulting vector \$\mathbf{b}\$? The answer is \$\mathbf{x} = \begin{bmatrix} 1 \\\\ 1 \end{bmatrix}\$, or
1 times of the first column plus 1 times the second column of \$\mathbf{A}\$.

<br>

## Linear Combination of Rows

There is also a similar perspective that can be applied to the rows of \$\mathbf{A}\$. For example, note the following
equation:

$$
\begin{bmatrix}
	x_1 & x_2 \\
\end{bmatrix}
\begin{bmatrix}
	1 & 2 \\
	1 & 0 \\
\end{bmatrix}
=
\begin{bmatrix}
	3 & 2 \\
\end{bmatrix}
$$

This can be seen as:

$$
x_1
\begin{bmatrix}
	1 & 2 \\
\end{bmatrix}
+
x_2
\begin{bmatrix}
	1 & 0 \\
\end{bmatrix}
=
\begin{bmatrix}
	3 & 2 \\
\end{bmatrix}
$$

or simply which **linear combination** of the **rows** of \$\mathbf{A}\$ will yield the row vector
\$\begin{bmatrix} 3 & 1 \end{bmatrix}\$. And that is $\mathbf{x} = \begin{bmatrix} 1 & 2 \end{bmatrix}\$, or
1 times of the first row plus 2 times the second row of \$\mathbf{A}\$.

This perspective can also be used in matrix multiplications. Consider the following equation of \$\mathbf{AB} =
\mathbf{C}\$:

$$
\begin{bmatrix}
	1 & 0 \\
	2 & 1 \\
\end{bmatrix}
\begin{bmatrix}
	1 & 2 \\
	1 & 0 \\
\end{bmatrix}
=
\begin{bmatrix}
	1 & 2 \\
	3 & 4 \\
\end{bmatrix}
$$

The usual method of calculating matrix multiplications would be:

$$
\begin{bmatrix}
	\mathbf{r_1} \\
	\mathbf{r_2} \\
\end{bmatrix}
+ 
\begin{bmatrix}
	\mathbf{c_1} & \mathbf{c_2} \\
\end{bmatrix}
=
\begin{bmatrix}
	\mathbf{r_1} \cdot \mathbf{c_1} & \mathbf{r_1} \cdot \mathbf{c_2} \\ 
	\mathbf{r_2} \cdot \mathbf{c_1} & \mathbf{r_2} \cdot \mathbf{c_2}
\end{bmatrix}
$$

With our new perspective of linear combination of rows, the matrix multiplication of \$\mathbf{AB} = \mathbf{C}\$ can
be seen this way:

$$
\begin{align}
	\begin{bmatrix}
		1 & 0 \\
		2 & 1 \\
	\end{bmatrix}
	\begin{bmatrix}
		1 & 2 \\
		1 & 0 \\
	\end{bmatrix}
	&=
	\begin{bmatrix}
		1 \times  \textrm{$1^{\textrm{st}}$ row of $\mathbf{B}$} + 0 \times \textrm{$2^{\textrm{nd}}$ row of $\mathbf{B}$} \\
		2 \times  \textrm{$1^{\textrm{st}}$ row of $\mathbf{B}$} + 1 \times \textrm{$2^{\textrm{nd}}$ row of $\mathbf{B}$} \\
	\end{bmatrix}
	\\
	&=
	\begin{bmatrix}
		1 & 2 \\
		2 & 4 \\
	\end{bmatrix}
\end{align}
$$

This is very useful in obtaining elementary matrices for elementary row operations. For example, to reduce the following
matrix into row echelon form, you subtract 2 times of the 2<sup>nd</sup> row from the 3<sup>rd</sup> row:

$$
\begin{bmatrix}
	1 & 3 & 0 \\
	0 & 2 & 1 \\
	0 & 4 & 3 \\
\end{bmatrix}
\xrightarrow{R_3 - 2R_2}
\begin{bmatrix}
	1 & 3 & 0 \\
	0 & 2 & 1 \\
	0 & 0 & 1 \\
\end{bmatrix}
$$

Equivalently, this elementary row operation can be represented by the pre-multiplication of the target matrix with an
elementary matrix. How then is this elementary matrix derived? Exactly the same way using the perspective of a **linear
combination** of **rows** as explained above. Let's first look at the first row. Since the first row is untouched, this
corresponds to 1 times the first row and 0 times the second and third row, giving \$\begin{bmatrix} 1 & 0 & 0
\end{bmatrix}\$ as the first row of the elementary matrix. The same principle applies for the second row, giving
\$\begin{bmatrix} 0 & 1 & 0 \end{bmatrix}\$. Deriving the final row is equally as simple with this principle, in fact,
it is the exact translation of the elementary row operation from words into a row vector multiplication: 
\$ 0R_1 - 2R_2 + 1R_3 \$, giving \$\begin{bmatrix} 0 & -2 & 1 \end{bmatrix}\$. Thus, this gives the following elementary
matrix:

$$
\begin{bmatrix}
	1 & 0 & 0 \\
	0 & 1 & 0 \\
	0 & -2 & 1 \\
\end{bmatrix}
\begin{bmatrix}
	1 & 3 & 0 \\
	0 & 2 & 1 \\
	0 & 4 & 3 \\
\end{bmatrix}
=
\begin{bmatrix}
	1 & 3 & 0 \\
	0 & 2 & 1 \\
	0 & 0 & 1 \\
\end{bmatrix}
$$

I hope that this was an interesting read to you! :)

