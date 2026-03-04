The main idea of Bayesian ranking is to treat the variables in a Bayesian approach. The random variable is sampled from a random distribution, however, the parameters of said distribution are also randomly distributed.
- Start with some likelihood function
- Choose a prior distribution
- Calculate the posterior distribution
- Sample from posterior for ranking
In particular, we sample from the posterior only if we are looking to do recommendations, as this would automatically balance the explore-exploit dilemma. Meanwhile for ranking, we are more interested in the averages of the distributions. For ranking however, we should filter out those with very few ratings to ensure that the ranking is actually accurate. We should not do this for a recommender system however, as that will defeat the purpose of balancing explore-exploit.

# Implementations
`Pseudo-Bernoulli`
To simplify this we will use a conjugate prior as the corresponding posteriors are incredibly easy to find. We will consider ranking movies based on user ratings. In particular, we will treat the rating as a sort of Bernoulli model. So a rating of 5 means 10 successes in 10 trials, and 0 means 0 successes in 10 trials. This is incorrect and does not represent the actual reality but is an indicative example. We are essentially creating information out of nowhere.

`Bernoulli`
We have also done another one where ratings are considered to be likes or dislikes. We choose a threshold such that ratings above it are likes and the rest are considered dislikes. In this case then we can apply a beta prior in an actually appropriate manner. Note however that depending on the chosen threshold, it may affect our results and our overall ranking, so it is still not as good as it could be. 

`Multinomial`
Extending on the previous ideas, we can extend the distributions into their multivariate forms. We will consider ratings to be a multinomial distribution and thus we will use its conjugate prior the Dirichlet distribution (multivariate form of the beta distribution).