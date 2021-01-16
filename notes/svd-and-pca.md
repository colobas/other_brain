---
title: SVD and PCA
layout: tree
---

# Tags
[algebra](20201114230107-algebra.md) [decomposition](decomposition.md)


# ,,,,blank,,,,

This is a two-part post, with some notes I wrote while refreshing the
concepts of SVD and PCA.


# Singular Value Decomposition


## ,,,,blank,,,,

Take any matrix \\(A\\). Generally speaking, what it does to a vector
\\(\vec{x}\\) is stretch it and rotate it.


## ,,,,blank,,,,

Now let&rsquo;s consider what a matrix \\(A\\) does to a unitary circle:
![img](/images/matrix-multiplication.png)


### ,,,,blank,,,,

The orthonormal vectors \\(\vec{v\_1}\\) and \\(\vec{v\_2}\\) were rotated into
the orthonormal vectors \\(\vec{u\_1}\\) and \\(\vec{u\_2}\\) and scaled by some
constants, \\(\sigma\_1\\) and \\(\sigma\_2\\)


### ,,,,blank,,,,

This is equivalent to saying \\(AV = U\Sigma\\), where \\(V\\) has the vectors
\\(\vec{v}\\) in its columns, and \\(U\\) has the vectors \\(\vec{u}\\) in its
columns.

\begin{align\*}
AV &= \hat{U}\hat{\Sigma} \\\\\\
A &= \hat{U}\hat{\Sigma} V^\*
\end{align\*}

(Becaue \\(V\\) is orthonormal, its inverse is the same as its tranpose)

1.  ,,,,blank,,,,

    This is called the reduced Singular Value Decomposition. More visually:
    
    \\[\underbrace{\begin{bmatrix}
    & & \\\\\\
    & A &\\\\\\
    & & \\\\\\
    \end{bmatrix}}\_{(m\times n)}
    \underbrace{\begin{bmatrix}
    \vert & \vert & & \vert\\\\\\
    \vec{v\_1} & \vec{v\_2} & ... & \vec{v\_n}\\\\\\
    \vert & \vert & & \vert\\\\\\
    \end{bmatrix}}\_{(n\times n)} =
    \underbrace{\begin{bmatrix}
    \vert & \vert & & \vert\\\\\\
    \vec{u\_1} & \vec{u\_2} & ... & \vec{v\_m}\\\\\\
    \vert & \vert & & \vert\\\\\\
    \end{bmatrix}}\_{(m\times n)}
    \underbrace{\begin{bmatrix}
    \sigma\_1 & & \\\\\\
    & \ddots & \\\\\\
    & & \sigma\_n \\\\\\
    \end{bmatrix}}\_{(n\times n)}\\]

2.  ,,,,blank,,,,

    Equivalently:
    
    \\[
    \underbrace{\begin{bmatrix}
    & & \\\\\\
    & & \\\\\\
    & A &\\\\\\
    & & \\\\\\
    & & \\\\\\
    \end{bmatrix}}\_{(m\times n)} = 
    \
    \underbrace{\begin{bmatrix}
    & & \\\\\\
    & & \\\\\\
    & \hat{U} &\\\\\\
    & & \\\\\\
    & & \\\\\\
    \end{bmatrix}}\_{(m\times n)}
    \
    \underbrace{\begin{bmatrix}
    \ & & \\\\\\
    \ & \hat{\Sigma} &\\\\\\
    \ & & \\\\\\
    \end{bmatrix}}\_{(n\times n)}
    \
    \underbrace{\begin{bmatrix}
    & & \\\\\\
    & V^\* &\\\\\\
    & & \\\\\\
    \end{bmatrix}}\_{(n\times n)}
    \\]

3.  ,,,,blank,,,,

    Since \\(\hat{U}\\) is underdetermined, normally we work with:
    
    \begin{align\*}
    \underbrace{\begin{bmatrix}
    & & \\\\\\
    & & \\\\\\
    & A &\\\\\\
    & & \\\\\\
    & & \\\\\\
    \end{bmatrix}}\_{(m\times n)} = 
    \
    \underbrace{
    \left[
    \begin{array}{c c c|c c}
    & & & & \\\\\\
    & & & & \\\\\\
    & \hat{U} & & &\\\\\\
    & & & & \\\\\\
    & & & & \\\\\\
    \end{array}
    \right]
    }\_{\stackrel{\mathbf U}{(m\times m)}}
    \
    \underbrace{\begin{bmatrix}
    \ & & \\\\\\
    \ & \hat{\Sigma} &\\\\\\
    \ & & \\\\\\
    \hline
    \ 0 & ...  & 0 \\\\\\
    \ 0 & ... & 0 \\\\\\
    \end{bmatrix}}\_{\stackrel{\mathbf\Sigma}{(m\times n)}}
    \
    \underbrace{\begin{bmatrix}
    & & \\\\\\
    & V^\* &\\\\\\
    & & \\\\\\
    \end{bmatrix}}\_{(n\times n)}
    \end{align\*}

4.  ,,,,blank,,,,

    I.e., \\(U\\) is obtained by adding \\((m-n)\\) orthonormal columns to \\(\hat U\\),
    and \\(\Sigma\\) is obtained by adding \\((m-n)\\) rows of zeros to \\(\hat\Sigma\\)

5.  ,,,,blank,,,,

    Computing the SVD, boils down to finding the eigendecompositions of
    \\(AA^T\\) and \\(A^T A\\). The eigenvectors of \\(AA^T\\) are \\(U\\), and the
    eigenvectors of \\(A^T A\\) are \\(V\\). The eigenvalues of both \\(AA^T\\) and
    \\(A^T A\\) are the squares of the singular values! <span class="underline">\_</span>


# PCA


## ,,,,blank,,,,

Let \\(X\\) be a (centered) \\(m \times n\\) data matrix. Then
\\(\frac{1}{n-1} XX^T\\) is the corresponding covariance matrix.


## ,,,,blank,,,,

If there are non-zero off-diagonal values in the covariance matrix, that
means that the coordinates we picked have some redundancy. Let this
notion sink in. There are many ways to think about this, but it all
boils down to the fact that, if there are non-zero off-diagonal values
in the cov. matrix, then the coordinates we&rsquo;re using are not orthogonal.


### ,,,,blank,,,,

Why does this matter? Because if we have orthogonal coordinates, we know
that these are the directions of greates variation (hence &ldquo;Principal
Components&rdquo;), and in a lucky scenario, we might even find that we need
less dimensions to represent the data at hand. (For an excelent example
of this, and a lecture much better than my notes, check [this video](https://www.youtube.com/watch?v=a9jdQGybYmE) by Prof. J.
Nathan Kutz)


## PCA&rsquo;s goal

Find a coordinate system where the covariance matrix is diagonal.


## Approach 1


### ,,,,blank,,,,

\\(XX^T\\) is square and symmetric. It is possible to do eigendecomposition
on it:

\begin{align\*}
XX^T = S \Lambda S^{-1}
\end{align\*}


### ,,,,blank,,,,

Now take the following transformation: \\(Y = S^T X\\). Recall that the
columns of \\(S\\) are orthogonal, so \\(S^T = S^{-1}\\). Then, the covariance
matrix in the new space is:

\begin{align\*}
\frac{1}{n-1} YY^T &=  \frac{1}{n-1} S^T XX^T S \\\\\\
&= \frac{1}{n-1} S^T S \Lambda S^{-1} S \\\\\\
&= \frac{1}{n-1} \Lambda
\end{align\*}


### ,,,,blank,,,,

And we know \\(\Lambda\\) is diagonal, so we successfully found a coordinate
transform where off-diagonal values of the covariance matrix are 0,
hence minimizing redundancy.


### ,,,,blank,,,,

Remember: to obtain \\(Y\\), we hit \\(X\\) with \\(S^T\\). What&rsquo;s the
interpretation of this?

1.  If \\(Y = S^T X\\), then \\(X = SY\\),

2.  Which means that to &ldquo;translate&rdquo; from \\(Y\\) to \\(X\\) we use \\(S\\) as our change-of-basis matrix.

3.  Conversely, doing \\(Y = S^T X\\), translates \\(X\\) into the column-space of \\(S\\).

4.  And the columns of \\(S\\) are the eigenvectors of \\(XX^T\\)!


### ,,,,blank,,,,

So, in summary, the coordinate system in which redundancy is minimized
is precisely the one given by the eigenvectors of \\(XX^T\\)!

(Speaking of redundancy, this last chunk is a good example of that, but
writing it down like that does help consolidate things)


## Approach 2


### ,,,,blank,,,,

Same setting, but let&rsquo;s use the two following points:

-   \\(X = U\Sigma V^\*\\)
-   \\(Y = U^\* X\\)


### ,,,,blank,,,,

In this case, the covariance matrix in the \\(Y\\) space is:

\begin{align\*}
\frac{1}{n-1} YY^T &= \frac{1}{n-1} (U^\* X)(U^\* X)^T \\\\\\
&= \frac{1}{n-1} (U^\* X)(X^\* U)\\\\\\
&= \frac{1}{n-1} U^\* (X)(X^\*) U\\\\\\
&= \frac{1}{n-1} U^\* (U\Sigma V^\*)(V \Sigma^T U^\*) U \\\\\\
&= \frac{1}{n-1} (U^\*U) \Sigma (V^\*V) \Sigma^T (U^\* U) \\\\\\
&= \frac{1}{n-1} \Sigma\Sigma^T
\end{align\*}

1.  ,,,,blank,,,,

    Where I&rsquo;ve repeated some of the steps with the parenthesis in different
    locations, to make things clearer.


### ,,,,blank,,,,

You can easily see that \\(\Sigma \* \Sigma^T\\) is diagonal (its last
\\((m-n)\\) diagonal elements are going to be zero).


### ,,,,blank,,,,

Again, what&rsquo;s the meaning of this? Following the same rationale, we&rsquo;re
saying that \\(U^\*\\) is a change-of-basis matrix that takes us to a space
where the covariance matrix is diagonal. If you paid attention, you&rsquo;ll
notice that the columns of \\(U\\) are precisely the eigenvectors of
\\(XX^T\\) - the coordinate system we arrived at, in the previous section.
So there&rsquo;s the connection between the two approaches. (You could have
guessed it by the fact that we normally think of computing the
eigendecomposition of \\(XX^T\\) and \\(X^T X\\)).


## TL;DR

Given a data matrix \\(X\\), the principal directions of variation
in that data are given by the eigenvectors of its covariance matrix, and
the magnitude of variation in each of those directions is given by the
eigenvalues of the covariance matrix.
