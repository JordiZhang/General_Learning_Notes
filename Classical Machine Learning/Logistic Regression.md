Logistic regression is essentially an extension to the linear model. We define the sigmoid function:
$$\sigma (x)=\frac{1}{1+e^{-x}}$$
![[Logres.png]]
The sigmoid function has the properties that it is always between 0 and 1. It approaches 1 at $\infty$ and -1 at $-\infty$. Then the logistic model is:
$$p(y=1|x)=\sigma(w^Tx+b)$$
Note however, that this model only discriminates between two classes, where we are modelling the probability of the data being part of a certain class, represented by $1$.
# Multiclass Logistic Regression
Also called Multinomial Logistic Regression or Maximum Entropy Classifier. Suppose we have $k$ classes. Instead of having one bias and one weight vector, we instead have $k$ such ones.
$$w_1, w_2,...,w_k\qquad b_1,b_2,...,b_k$$
Then instead of using the sigmoid function, we utilize the Softmax function:
$$\text{softmax}(a)_k=\frac{\exp(a_k)}{\sum_{j=1}^K \exp(a_j)} \qquad \text{for }k=1,2,...,K$$
where $a_k =w^T_k x +b_k$. So the probabilities are:
$$p(y=k|x)=\text{softmax}(a)_k$$
We can think of the Softmax as a sort of higher dimension version of the sigmoid function. Although this is inaccurate.