From the collaborative filtering section, we have seen that the user-item matrix is the key part of the whole algorithm. However, we have also seen the main problems in working with it, namely its huge size and its sparcity. In general, it is unfeasible to store the entirety of the matrix unless we use some data structure to represent it. In our case, we utilized a sparse representation implemented via scipy. 

The idea behind this section is to be able to represent the entire matrix in a different manner. Instead we look to approximate the user-item matrix as the product of 2 much smaller matrices.
$$\hat{R}=WU^T$$
We would like W and U to be very skinny/elongated so that $W(N\times K)$ and $U(M\times K)$. Usually $K$ is somewhere between 10-50, it is thus a hyperparameter of the model. Thus if we want to access a certain rating,
$$\hat{r}_{ij}=\hat{R}[i,j]=w_i^Tu_j,\qquad w_i=W[i],\qquad u_j=U[j]$$
Note that if $K=M$ then this factorization is exact and is not an approximation. However, by reducing $K$ we are using a dimensionality reduction technique and we encourage the model to learn the most important features to generate the user-item matrix.
# Training
How can we ensure a good approximation? 
First we would want to define a loss function as always. Since this is a regression problem, the mean squared error is appropriate. However, since the denominator is simply the size, so it is a constant. We can drop it and simply use the squared error as our loss. Again the goal is to minimize the loss, so differentiate and set to 0. 

Let $J$ be the squared error, i.e. the loss. $\Omega$ being the set of all users and items.
$$J=\sum_{i,j\in\Omega}(r_{ij}-\hat{r}_{ij})^2=\sum_{i,j\in\Omega}(r_{ij}-w_i^Tu_j)^2$$
$$\frac{\partial J}{\partial w_i}=2\sum_{j\in \Psi_i}(r_{ij}-w_i^Tu_j)(-u_j)=0$$
Where $\Psi_i$ is the set of items that user $i$ has rated.
$$\sum_{j\in\Psi_i}(w_i^Tu_j)u_j=\sum_{j\in\Psi_j}r_{ij}u_j$$
Dot product is commutative, so $w_i^Tu_j=u_j^Tw_i$. Also the result of a dot product is a scalar, so we are free to move around the dot product. Therefore we have:
$$\sum_{j\in\Psi_i}u_j(u_j^Tw_i)=\sum_{j\in\Psi_j}r_{ij}u_j$$
$$\left(\sum_{j\in\Psi_i}u_ju_j^T\right)w_i=\sum_{j\in\Psi_i}r_{ij}u_j$$
This is in the form $Ax=b$ which is solvable by inverting $A$. In code this is just
```Python
x = np.linalg.solve(A,b)
```
Repeating this calculation for $u_j$ we obtain a similar expression, both are shown below.
$$w_i=\left(\sum_{j\in\Psi_i}u_ju_j^T\right)^{-1}\sum_{j\in\Psi_i}r_{ij}u_j,\qquad u_j=\left(\sum_{i\in\Psi_j}w_iw_i^T\right)^{-1}\sum_{i\in\Psi_j}r_{ij}w_i$$
We have coupled equations, so we can't just solve for the parameters that will give us the minimum loss. Instead we can use these formulae iteratively as our training algorithm. We initialize the training algorithm with some random matrix W and U, and then apply the formulae over and over. 
```Python
W = random_matrix(N, K)
U = random_matrix(M, K)
for t in range(T):
	update_w
	update_u
```
The order in which you update first does not matter. Should we use the old values of w when updating u? It doesn't actually make a difference, however, using the new values is faster as we do not need to keep a copy of the old W. This sort of training algorithm is also called alternating least squares.