Consider the Pearson coefficient:
$$\rho_{i_x i_y}=\frac{\sum_{i=1}^n\left(x_i-\bar{x}\right)\left(y_i-\bar{y}\right)}{\sqrt{\sum_{i=1}^n\left(x_i-\bar{x}\right)^2} \sqrt{\sum_{i=1}^n\left(y_i-\bar{y}\right)^2}}$$
We want to obtain the Pearson Coefficient Matrix from the user movie matrix, we could do this by looping over the matrix and calculating the coefficient for every user-user pair, but this is inefficient. Instead we can utilize some smart linear algebra to obtain this in a faster way.

Lets write the Pearson Coefficient in vector notation.
$$\rho_{x,y}=\frac{(r_x-\mu_x)\cdot(r_y-\mu_y)}{||r_x-\mu_x||]\text{ } ||r_y-\mu_y||}$$
We will separate the numerator and denominator. 
# Numerator
Lets call the user movie matrix R. We first mean-center the matrix, so we calculate the means of each row (i.e. each user) and subtract from the matrix R to obtain a new matrix M.
$$M = R-\mu$$
Now we can simply multiply the matrix by its transpose to obtain the numerator. We call this matrix S, for similarity.
$$S = MM^T$$
Each row-column combination of this corresponds to its given 
$$(r_x-\mu_x)\cdot(r_y-\mu_y)$$
# Denominator
We want to make an array that holds the norms of each row vector in the user movie matrix. To do so, we calculate it the usual way, square each element, sum it up and square root. We now take the element-wise inverse of the norms and we create a new matrix whose diagonal elements are the inverse norms.
$$
D^{-1}=\left[\begin{array}{ccc}
1 /\left\|r_1-\mu_1\right\| & 0 & 0 \\
0 & 1 /\left\|r_2-\mu_2\right\| & 0 \\
0 & 0 & 1 /\left\|r_3-\mu_3\right\|
\end{array}\right]
$$
Now we can do a nice little trick with matrix multiplication. 
$$
\left(D^{-1} S\right)[x, y]=\frac{1}{\left\|r_x-\mu_x\right\|} S[x, y]
$$
Right multiply:
$$
\left(S D^{-1}\right)[x, y]=S[x, y] \frac{1}{\left\|r_y-\mu_y\right\|}
$$
So doing both:
$$
\left(D^{-1} S D^{-1}\right)[x, y]=\frac{S[x, y]}{\left\|r_x-\mu_x\right\|\left\|r_y-\mu_y\right\|}
$$
Which is exactly the Pearson Correlation Matrix.