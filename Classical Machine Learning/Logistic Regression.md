Logistic regression is essentially an extension to the linear model. We define the sigmoid function:
$$\sigma (x)=\frac{1}{1+e^{-x}}$$
![[Logres.png]]
The sigmoid function has the properties that it is always between 0 and 1. It approaches 1 at $\infty$ and -1 at $-\infty$. Then the logistic model is:
$$p(y=1|x)=\sigma(w^Tx+w_{0})$$
Note however, that this model only discriminates between two classes, where we are modelling the probability of the data being part of a certain class, represented by $1$. Even though it is a regression technique, its incredibly useful as a probabilistic classifier. Depending on whether we are performing regression or classification, our definition of logistic regression may change. As a classifier we want the output to be the predicted class, so $y$ is useful, as a regression problem we want the probability $p(y=1|x)$.
# Finding the Weights
In linear regression we use the Squared Errors or the MSE equivalently, while this works if the goal is regression, we often use logistic regression for classification. In that case the MSE makes no sense to use. Instead we define the (Binary) Cross-Entropy Loss function:
$$
BCE=-\frac{1}{N}\sum_{i=1}^{N}(y_{i}\log p_{i}+(1-y_{i})\log(1-p_{i})) 
$$
Since $y$ is the predicted class and it can only be either $1$ or $0$, only one of the two terms in the sum matters at a time. Then the closer the probability is to the target, the less loss there is.

When using the logistic model for classification, we obtain probabilities of each data point (out of $N$ points) being a certain class. Then each point follows a Bernoulli distribution with probability given by the logistic regression. Therefore we obtain the likelihood:
$$L_{\text{likelihood}}=\prod_{i=1}^{N} p_{i}^{y_{i}}(1-p_{i})^{1-y_{i}}$$
Taking the logarithm:
$$
L_{\text{likelihood}}=\sum_{i=1}^{N}(y_{i}\log p_{i}+(1-y_{i})\log(1-p_{i}) )
$$
Thus maximizing the likelihood is equivalent to minimizing the BCE. 

In general the BCE does not have a closed form solution for the minimum, so instead we utilize gradient descent. We can obtain a closed form for the gradient by differentiating with respect to the weights and bias, and applying chain rule. Then recognizing that sum of products is equivalent to inner products we obtain the matrix form of the gradient:
$$\nabla _{w}L=X^T(P-Y)$$
# Multiclass Logistic Regression
Also called Multinomial Logistic Regression or Maximum Entropy Classifier. Suppose we have $k$ classes. Instead of having one bias and one weight vector, we instead have $k$ such ones.
$$w_1, w_2,...,w_k\qquad b_1,b_2,...,b_k$$
Then instead of using the sigmoid function, we utilize the Softmax function:
$$\text{softmax}(a)_k=\frac{\exp(a_k)}{\sum_{j=1}^K \exp(a_j)} \qquad \text{for }k=1,2,...,K$$
where $a_k =w^T_k x +b_k$. So the probabilities are:
$$p(y=k|x)=\text{softmax}(a)_k$$
We can think of the Softmax as a sort of higher dimension version of the sigmoid function. Although this is inaccurate.

In a similar manner, the weights can be obtained via the Categorical Cross Entropy, also known as the Softmax Loss.
# Regularization
Essentially the same methodology and reasoning as for linear regression, we wish to prevent overfitting by penalizing weights accordingly. Add scaled norms of the weights vector to the BCE function, the loss. For L2:
$$
L=-\sum_{i=1}^{N}(y_{i}\log p_{i}+(1-y_{i})\log(1-p_{i}) )+\lambda||w||_{2}^2
$$
For L1:
$$
L=-\sum_{i=1}^{N}(y_{i}\log p_{i}+(1-y_{i})\log(1-p_{i}) )+\lambda||w||_{1}^2
$$