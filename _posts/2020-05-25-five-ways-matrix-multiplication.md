---
layout: post
title: "Five Ways of doing Matrix Multiplications"
author: "Yuan Bo Chen"
categories: learning
tags: [linear algebra, math]
---

Matrix multiplications form the backbone of many operations in Linear Algebra. While most of these calculations are
automated now using math libraries, it is still useful to understand the different ways of doing matrix multiplications
as they are often used in mathematical proofs in academic papers. So, I will talk about 5 different ways matrix
multiplication can be done in this article. Credit goes to the lovely Gilbert Strang and his amazing [lecture series](https://www.youtube.com/playlist?list=PL221E2BBF13BECF6C) on Linear Algebra.

<br>

## 1. The Standard Way

$$
\begin{bmatrix}
	\rule[.5ex]{2.5ex}{0.5pt} & \mathbf{r_1} & \rule[.5ex]{2.5ex}{0.5pt} \\
	\rule[.5ex]{2.5ex}{0.5pt} & \mathbf{r_2} & \rule[.5ex]{2.5ex}{0.5pt} \\
\end{bmatrix}
\begin{bmatrix}
	\rule[-1ex]{0.5pt}{2.5ex} & \rule[-1ex]{0.5pt}{2.5ex} \\
	\mathbf{c_1} & \mathbf{c_2} \\
	\rule[-1ex]{0.5pt}{2.5ex} & \rule[-1ex]{0.5pt}{2.5ex} \\
\end{bmatrix}
=
\begin{bmatrix}
	\mathbf{r_1} \cdot \mathbf{c_1} & \mathbf{r_1} \cdot \mathbf{c_2} \\ 
	\mathbf{r_2} \cdot \mathbf{c_1} & \mathbf{r_2} \cdot \mathbf{c_2}
\end{bmatrix}
$$

The first method is the method that most students are taught: generate each entry of the resultant matrix by taking the
dot product of the corresponding rows and columns of the multiplying matrices. This method is straightforward and did
carry me through the entirety of my linear algebra course, but it gives little intuition in complex mathematical proofs
used in specialized areas of computer science (e.g. computer vision).

<br>

## 2. As Linear Combination of Columns

The second way to do matrix multiplications is to see it as a **linear combination of columns** in the **left** matrix.
To illustrate, let's begin using a simple example. The following equation:

$$
\mathop{\begin{bmatrix}
	1 & 2 \\
	1 & 0 \\
\end{bmatrix}}_{\textstyle \mathbf{A}}
\mathop{\begin{bmatrix}
	x_1 \\
	x_2 \\
\end{bmatrix}}_{\textstyle \mathbf{x} \vphantom{A}}
=
\mathop{\begin{bmatrix}
	3 \\
	1 \\
\end{bmatrix}}_{\textstyle \mathbf{b} \vphantom{A}}
$$

can be equally expressed as:

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
3 \\\\ 1 \end{bmatrix}\$? Or simply put, what **linear combination** of the first and second column of \$\mathbf{A}\$
yields us the resulting vector \$\mathbf{b}\$? The answer is \$\mathbf{x} = \begin{bmatrix} 1 \\\\ 1 \end{bmatrix}\$, or
1 times of the first column plus 1 times the second column of \$\mathbf{A}\$.

<br>

This is the same with matrix multiplications of other sizes:

$$
\begin{align}
\mathop{\begin{bmatrix}
	1 & 0 \\
	2 & 1 \\
\end{bmatrix}}_{\mathbf{A}}
\mathop{\begin{bmatrix}
	1 & 2 \\
	1 & 0 \\
\end{bmatrix}}_{\mathbf{B}}
&=
\begin{bmatrix}
	1 & 0 \\
	2 & 1 \\
\end{bmatrix}
\begin{bmatrix}
	\mathbf{b_1} & \mathbf{b_2} \\
\end{bmatrix} \\

&=
\begin{bmatrix}
	\mathbf{Ab_1} & \mathbf{Ab_2}
\end{bmatrix} \\

\newline

\mathbf{Ab_1}
&=
1 \begin{bmatrix}
	1 \\
	2 \\
\end{bmatrix}
+
1 \begin{bmatrix}
	0 \\
	1 \\
\end{bmatrix}
=
\begin{bmatrix}
	1 \\
	3 \\
\end{bmatrix} \\

\mathbf{Ab_2}
&=
2 \begin{bmatrix}
	1 \\
	2 \\
\end{bmatrix}
+
0 \begin{bmatrix}
	0 \\
	1 \\
\end{bmatrix}
=
\begin{bmatrix}
	2 \\
	4 \\
\end{bmatrix} \\

\newline

\mathop{\begin{bmatrix}
	1 & 0 \\
	2 & 1 \\
\end{bmatrix}}_{\mathbf{A}}
\mathop{\begin{bmatrix}
	1 & 2 \\
	1 & 0 \\
\end{bmatrix}}_{\mathbf{B}}
&=
\begin{bmatrix}
	\mathbf{Ab_1} & \mathbf{Ab_2}
\end{bmatrix}
=
\begin{bmatrix}
	1 & 2 \\
	3 & 4 \\
\end{bmatrix}
\end{align}
$$

<br>

## 3. As Linear Combination of Rows

A similar perspective that can be applied to the rows of \$\mathbf{A}\$. For example, the following equation:

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

can be expressed as:

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

or simply what **linear combination** of the **rows** of \$\mathbf{A}\$ will yield the row vector
\$\begin{bmatrix} 3 & 1 \end{bmatrix}\$. And that is $\mathbf{x} = \begin{bmatrix} 1 & 2 \end{bmatrix}\$, or
1 times of the first row plus 2 times the second row of \$\mathbf{A}\$.

<br>

We can use the same example in method 2 to further examine this particular perspective:

$$
\begin{align}
\mathop{\begin{bmatrix}
	1 & 0 \\
	2 & 1 \\
\end{bmatrix}}_{\mathbf{A}}
\mathop{\begin{bmatrix}
	1 & 2 \\
	1 & 0 \\
\end{bmatrix}}_{\mathbf{B}}
&=
\begin{bmatrix}
	\mathbf{a^T_1} \\
	\mathbf{a^T_2} \\
\end{bmatrix}
\begin{bmatrix}
	1 & 2 \\
	1 & 0 \\
\end{bmatrix} \\

&=
\begin{bmatrix}
	\mathbf{a^T_1 B} \\
	\mathbf{a^T_2 B} \\
\end{bmatrix} \\

\newline

\mathbf{a^T_1 B}
&=
1 \begin{bmatrix}
	1 & 2 \\
\end{bmatrix}
+
0 \begin{bmatrix}
	1 & 0 \\
\end{bmatrix}
=
\begin{bmatrix}
	1 & 2 \\
\end{bmatrix} \\

\mathbf{a^T_2 B}
&=
2 \begin{bmatrix}
	1 & 2 \\
\end{bmatrix}
+
1 \begin{bmatrix}
	1 & 0 \\
\end{bmatrix}
=
\begin{bmatrix}
	3 & 4 \\
\end{bmatrix} \\

\newline

\mathop{\begin{bmatrix}
	1 & 0 \\
	2 & 1 \\
\end{bmatrix}}_{\mathbf{A}}
\mathop{\begin{bmatrix}
	1 & 2 \\
	1 & 0 \\
\end{bmatrix}}_{\mathbf{B}}
&=
\begin{bmatrix}
	\mathbf{a^T_1 B} \\
	\mathbf{a^T_2 B} \\
\end{bmatrix}
=
\begin{bmatrix}
	1 & 2 \\
	3 & 4 \\
\end{bmatrix}
\end{align}
$$

<br>

This is very useful in obtaining elementary matrices for elementary row operations. For example, to reduce the following
matrix into row echelon form, you subtract 2 times of the 2<sup>nd</sup> row from the 3<sup>rd</sup> row:

$$
\mathop{\begin{bmatrix}
	1 & 3 & 0 \\
	0 & 2 & 1 \\
	0 & 4 & 3 \\
\end{bmatrix}}_{\textstyle \mathbf{A}}
\xrightarrow{R_3 - 2R_2}
\mathop{\begin{bmatrix}
	1 & 3 & 0 \\
	0 & 2 & 1 \\
	0 & 0 & 1 \\
\end{bmatrix}}_{\textstyle \mathbf{R}}
$$

Equivalently, this elementary row operation can be represented by the pre-multiplication of \$\mathbf{A}\$ with an
elementary matrix. How then is this elementary matrix derived? Exactly the same way using the perspective of a **linear
combination** of **rows** as explained above. Since the first row is untouched, this
corresponds to 1 times the first row and 0 times the second and third row, giving \$\begin{bmatrix} 1 & 0 & 0
\end{bmatrix}\$ as row 1 of the elementary matrix. The same principle applies for the second row, giving
\$\begin{bmatrix} 0 & 1 & 0 \end{bmatrix}\$. Deriving the final row is equally as simple using this idea, in fact,
it is the exact translation of the elementary row operation from words into a row vector multiplication: 
\$ 0R_1 - 2R_2 + 1R_3 \$, giving \$\begin{bmatrix} 0 & -2 & 1 \end{bmatrix}\$. Thus, this gives the following elementary
matrix:

$$
\mathop{\begin{bmatrix}
	1 & 0 & 0 \\
	0 & 1 & 0 \\
	0 & -2 & 1 \\
\end{bmatrix}}_{\textstyle \mathbf{E}}
\mathop{\begin{bmatrix}
	1 & 3 & 0 \\
	0 & 2 & 1 \\
	0 & 4 & 3 \\
\end{bmatrix}}_{\textstyle \mathbf{A}}
=
\mathop{\begin{bmatrix}
	1 & 3 & 0 \\
	0 & 2 & 1 \\
	0 & 0 & 1 \\
\end{bmatrix}}_{\textstyle \mathbf{R}}
$$

The same idea applies for swapping of and taking multiple of rows. Note that if we were to do column operations instead,
the elementary matrix would have to be **post-multiplied** to the target matrix.

<br>

## 4. Sum of Columns times Rows

The fourth way is pretty interesting and not commonly seen, but it is done by taking the sum of the columns of the first
matrix multiplied by the rows of the second matrix. Note the specific order of taking the columns and rows: columns for
the first matrix, rows for the second. Let's first use a simple example to illustrate. We begin by multiplying a column
vector \$\mathbf{c}\$ to a row vector \$\mathbf{r}\$. This yields us a full-sized matrix \$\mathbf{M}\$ shown below:

$$
\mathop{\begin{bmatrix}
	2 \\
	3 \\
	4 \\
\end{bmatrix}}_{\textstyle \mathbf{c} \vphantom{\mathbf{M}}}
\mathop{\begin{bmatrix}
	1 & 6 \\
\end{bmatrix}}_{\rule{0pt}{2.95em} \textstyle \mathbf{r}}
=
\mathop{\begin{bmatrix}
	2 & 12 \\
	3 & 18 \\
	4 & 24 \\
\end{bmatrix}}_{\textstyle \mathbf{M}}
$$

Looking at the resultant matrix \$\mathbf{M}\$, there a two special properties about it: its rows are multiples of
\$\mathbf{r}\$ and its columns are multiples of \$\mathbf{c}\$. Put more rigorously, the **rowspace of \$\mathbf{M}\$
is spanned by \$\mathbf{r}\$** while the **columnspace of \$\mathbf{M}\$ is spanned by \$\mathbf{c}\$**.

<br>

Matrix multiplications in bigger dimensions is done using the sample principle:
1. Multiply the columns of the left matrix to the corresponding rows of the right matrix
2. Sum up the resultant matrices

Incidentally, this looks like the first method of doing matrix multplications, except compressed:

$$
\begin{align}
\mathop{\begin{bmatrix}
	1 & 0 \\
	2 & 1 \\
\end{bmatrix}}_{\mathbf{A}}
\mathop{\begin{bmatrix}
	1 & 2 \\
	1 & 0 \\
\end{bmatrix}}_{\mathbf{B}}
&=
\begin{bmatrix}
	\mathbf{a_1} & \mathbf{a_2} \\
\end{bmatrix}
\begin{bmatrix}
	\mathbf{b^T_1} \\
	\mathbf{b^T_2} \\
\end{bmatrix} \\

&=
\mathbf{a_1 b^T_1 + a_2 b^T_2} \\

&=
\begin{bmatrix}
	1 & 2 \\
	2 & 4 \\
\end{bmatrix}
+
\begin{bmatrix}
	0 & 0 \\
	1 & 0 \\
\end{bmatrix} \\

&=
\begin{bmatrix}
	1 & 2 \\
	3 & 4 \\
\end{bmatrix}
\end{align}
$$

<br>

## 5. Block Matrix Multiplication

The final method of doing matrix multiplications is by doing **block multiplication**. The idea behind this is the same
as the standard way of doing matrix multiplications except with blocks this time i.e. block row multiplied by block
columns. This works as long as the rows and columns of each mini-block matches up in the usual matrix multiplication
sense:

$$
\left[\begin{array}{@{}c|c@{}}
  \mathbf{A_1} & \mathbf{A_2} \\
\hline
  \mathbf{A_3} & \mathbf{A_4} \\
\end{array}\right]
\left[\begin{array}{@{}c|c@{}}
  \mathbf{B_1} & \mathbf{B_2} \\
\hline
  \mathbf{B_3} & \mathbf{B_4} \\
\end{array}\right]
=
\left[\begin{array}{@{}c|c@{}}
  \mathbf{A_1 B_1 + A_2 B_3} & \mathbf{A_1 B_2 + A_2 B_4} \\
\hline
  \mathbf{A_3 B_1 + A_4 B_3} & \mathbf{A_3 B_2 + A_4 B_4} \\
\end{array}\right]
$$

<br>

Thanks for reading till the end, I hope that this was helpful to you! :)

