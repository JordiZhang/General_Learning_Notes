Linear regression models linear relationships as:
$$\hat{y} = w_1x_1 +b$$
Or in higher dimensions:
$$\hat{y} = w^Tx +b$$
Since it is regression, MSE is a natural loss function to use. Minimizing it leads to the following:
$$\hat{b}=\bar{y}-\hat{w}^T\bar{x},\qquad \hat{w}=\frac{\text{Cov}(x,y)}{\text{Var}(x)}$$
Note that these are equivalent to the Maximum Likelihood Estimators. Linear regression models data as a normal distribution with a varying mean. The likelihood is thus a product of gaussians and the log-likelihood is a negative scaled version of the MSE plus some constant terms. Thus maximizing the log-likelihood is equivalent to minimizing the MSE loss.
# Coefficient of Determination
$$
R^2=1-\frac{\sum\left(y_{i}-\hat{y}_{i}\right)^2}{\sum\left(\hat{y}_{i}-\bar{y}\right)^2},
$$
The numerator in $R^2$ is the sum of square residuals, while the denominator is the total sum of squares (sum of square deviations from the mean). By interpreting this coefficient, we can determine whether a model is good or not. A negative value would imply that the errors are very large and that our model is worse than simply predicting the mean every time. A value of 0 implies that the model simply learnt the mean and nothing else. Finally a value of $R^2$ close to 1 implies very little error in the model.
# Multiple Linear Regression
This is the multiple input case where instead of having a single input, we now have a vector of inputs. Note that we can always rename $b$ to $w_0$ and thus absorbing the bias term into the weights vector. Then by appending $1$ to the feature vector $x$, 
$$\hat{y}=w^Tx = w_{0}+w_{1}x_{1}+w_{2}x_{2}+\dots$$
In this case, we still use the MSE as the loss and take derivatives as usual, which results in the following general solution for the MLE estimator for $w$:
$$w=(X^TX)^{-1}X^Ty$$
# Additional Considerations
Lets suppose we apply multiple linear regression to a dataset. Then we append to the feature vector a new feature which is just some random noise. How does the $R^2$ value behave after a regression is fitted? In fact, this random noise improves slightly the coefficient of determination. In theory, random noise should be completely uncorrelated to the output, but in practice, we have a finite number of data, so in fact there is some non-zero correlation. Hence the slight increase in $R^2$. Note however, that this does not necessarily mean the model is better.
# Regularization
Data in real life is not perfect and as such we may have outliers in our data. These are problematic due to them 'pulling' the line away from the main trend in order to minimize the loss. This is where regularization comes in. The idea is to penalize large weights in the weights vector. 
## L2 
$$
L=\sum^{N}_{n=1}(y_{i}-\hat{y}_{i})^2+\lambda||w||_{2}^2
$$
In L2 Regularization we penalize by adding the squared L2 norm of the weights vector. Minimizing this, we obtain the expression for the weights vector:
$$w=(X^TX+\lambda I)^{-1}X^Ty$$
This form of regularization is also called Ridge regularization and it is also mathematically equivalent to performing maximum a posteriori estimation of $w$ with a gaussian prior.
## L1
In general we want to have many more samples than the number of features, but this may not always be possible. Sometimes we may have very few samples and a lot of features. It is also common that not all these features are important to the trend and may just be noise. Earlier we saw that random noise will improve the $R^2$ score, however this does not necessarily mean a better model. The goal of L1 Regularization is to incentivize the model to select a small number of meaningful features to describe the trend. Most features will have a weight of 0 (noise) and only the important ones will have non zero weights. L2 regularization uses the L2 norm, so similarly we penalize by adding the L1 norms.
$$L=\sum^{N}_{n=1}(y_{i}-\hat{y}_{i})^2+\lambda||w||_{1}^2$$
This form of regularization is also called Lasso regularization, this also puts a prior on the weights $w$ so it is also a maximum a posteriori estimation of $w$ but using a Laplacian prior instead. Note that there is no closed form solution for the weights vector in this case, instead we use numerical methods such as gradient descent.

Lastly it is also possible to combine both L1 and L2 into the so called ElasticNet.