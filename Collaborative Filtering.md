# User-User

|       | Batman | X-Men | Star Wars | The Notebook | Bridget Jones |
| ----- | ------ | ----- | --------- | ------------ | ------------- |
| Alice | 5      | 4.5   | 5         | 2            | 1             |
| Bob   | 4.5    | 4     |           | 2            | 2             |
| Carol | 2      | 3     | 1         | 5            | 5             |
Intuitively, from the above table, we would expect Bob to also enjoy Star Wars since his ratings are quite similar to Alice's ratings in which she has watched Star Wars and rated highly. We can assume Alice and Bob's tastes in movies are quite similar and thus highly correlated. We will try to create a scoring system that takes these into account so that the score depends both on the user and the movie.

## Average Rating
A naïve approach would be to use the average rating of movies. 
$$s(j)=\frac{\sum_k r_{k}}{n},\qquad r_i\in\Omega_j$$
Where $s(j)$ is the score, $r_k$ the ratings for a given movie $\Omega_j$ and $n$ the total number of users who rated the movie. $i$ denotes user dependence and $j$ denotes item dependence (movie in this case). So dependence on the movie but no dependence on user.

This has a few critical downfalls. Namely that it treats everyone's ratings in the same manner. Clearly this does not make sense since Carol disliking Star Wars shouldn't matter that much when we are making a recommendation for Bob (Note however that in this case Carol is highly negatively correlated so it does actually matter). The other downfall is that it does not solve the problem of explore-exploit. A single 5 star rating would rank higher than 1000s of 4.5 star ones. Another issue is that different people interpret ratings differently. An optimist may rate most things highly and very few lowly.
## Weighted Rating
We can go a step further by adding weights, i.e. a weighted average. Intuitively, correlated users should have a higher weight than those that aren't.
$$s(i,j)=\frac{\sum_k w_k(i)r_k}{\sum_k w_k(i)},\qquad r_k\in\Omega_j$$
Clearly this is a better scoring system than the simple average rating
## Deviation
Considering the average rating showed us some of the problems of the system. Different people rate things differently even within the same rating system, some people overrate things consistently and others may underrate things consistently. So instead of the absolute rating, we care about the deviation from the user's average.
$$dev(i,j)=r(i,j)-\bar{r}_i$$
Where $\bar{r}_i$ is the average rating for a given user. Then we can use this idea to predict a user's rating upon watching said movie. We can calculate the average deviation for all users for a given movie:
$$\hat{dev}(i,j)=\frac{1}{|\Omega_j|}\sum_{k}[r(k,j)-\bar{r}_k]$$
I.e. the sum of the deviations of each user for a given movie divided by the total number of users who rated said movie. Then we the predicted rating for a new user is their own average + the predicted deviation which is the average deviation for that movie.
$$s(i,j)=\bar{r}_i+\hat{dev}(i,j)$$
For the purpose of recommending new items, there is no need to actually calculate $s(i,j)$, the deviation alone is sufficient since the average that is being added is the same for all items.
## Combine Everything
Using the idea of deviation we have a much better way of ranking things. However, it still does not take into account users, some user ratings are more important than others depending on who the user we are making recommendations to is. So we combine the idea of deviations with the weighted rating, so we apply weights to each deviation.
$$s(i,j)=\bar{r}_i+\frac{\sum_kw_k(i)[r(k,j)-\bar{r}_k]}{\sum_k|w_k(i)|}$$
Weights can be negative, hence why we take the absolute value when calculating the normalizing constant.

Naturally the question is how do we calculate the weights. As mentioned earlier, we want a higher weight for users who are highly correlated and a lower one for those who aren't. It is then natural to use Pearson's Correlation Coefficient as our weights.
$$\rho_{i_x,i_y}=\frac{Cov(i_x, i_y)}{\sigma_{x}\sigma_y}$$
Where $i_x$ and $i_y$ are 2 different users, note that the correlation is calculated from the movies that both users have rated, i.e. those in common. This however introduces new problems.
- What if 2 users have no movies in common, or just a few?
- If zero, then we don't consider that user for the purpose of calculating the deviation, i.e. set the weight to zero
- If few, then similarly we don't consider it and set the weight to zero
- We do this because these users would likely provide inaccurate results. 
- Then the question is what threshold do we choose to discard users? This becomes a hyperparameter of the model.
## Neighbourhood
In practice, we don't sum over all users who rated a movie, this would take too long since the problem is $O(n^2)$, but also we would want to precompute the weights beforehand. Instead we might want to only use the top $k$ users with the highest weights. We call these the $k$-nearest neighbours (usually between 25-50). The reason for this name is that since the weights are the correlation coefficients, the ones with the highest weights have highest correlation and thus are closest in the coefficient space.
# Item-Item
Item-item collaborative filtering is mathematically equivalent to user-user filtering. Simply transpose your user-item matrix when doing the calculations. In practice however, item-item tends to be both faster and more accurate. It is faster since user-user is $O(N^2M)$ whereas item-item is $O(NM^2)$. It is usually the case that there are more users than items, hence a lower complexity for item-item. Even though item-item is usually more accurate than user-user in terms of MSE, this isn't necessarily a good thing as it might mean the algorithm only gives the obvious recommendations.