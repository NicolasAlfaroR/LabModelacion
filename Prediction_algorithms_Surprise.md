# Surprise prediction algorithms

Surprise is a Python library created by [Nicolas Hug](http://nicolas-hug.com) with the purpose of building and analyze recommender systems. Due to the improvement done by the Surprise's community regard their recommender system, in addition to don't falling in the "reinventing the wheel" crime, we will use some prediction algorithms based in the context of retail.


More about this library can be founded in [link](https://github.com/NicolasHug/Surprise) or [link2](http://surpriselib.com)

## Prediction algorithms Table:

* [Normal Predictor](#NormalPredictor)
* [Basic K-Nearest Neighbors](#Basic-K-Nearest-Neighbors)
	* [KNN Basic](#KNNBasic)
	* [KNN With Means](#KNNWithMeans)
	* [KNN With Zscore](#KNNWithZscore)
* [Co-clustering](#co-clustering)
* [SlopeOne](#Slope-One)

<br/><br/>

### NormalPredictor

1. <b> Overall mathematical description </b>: The NormalPredictor algorithm, is the simplest algorithm that predicts rating in a random way, assuming that the rating distribution is <ins> normal </ins> [<img src="https://latex.codecogs.com/gif.latex?\mathcal{N}(\mu,\sigma^2)" />], The parameters <img src="https://latex.codecogs.com/gif.latex?\mu,\sigma" /> are obtained through the Maximum likelihood estimation (Basically that under the assumed statistical model the observed data is most probable).
2. <b> Assumptions </b>: Assumes that the distribution of the rating is normal.
3. <b>Pros and Cons </b>
	* Pros: Easiest predictor, intuitive and fast.
	* Cons: Worst predictions,  performance strongly linked to variability.
	
<br/><br/>

## Basic K-Nearest Neighbors	

The next 3 algorithms are basically the same, In other words the procedure to predict the ratings are quite similar based in "k-nearest neighbors approach", The only 2 things that are changed is how we measure proximity or identify the neighborhoods, this parameter is named <ins> Similarity measure </ins>, the other difference is if user-information is considered (like his mean rating).

The basic K-Nearest Neighbors (KNN) approach works in the next way:

	1. Is defined the Similarity measure,the user and item of interest
	2. Calculate the Similarity measure for all other users (or items) that have rated the item (have been rated by the user).
	3. Sort in descending way and select the first k similar users (or items).
	4. Predict the rating relying on the previous list of similar users.

Knowing this, the next KNN algorithms differ in the step 4.


### KNNBasic

1. <b> Overall mathematical description </b>: As was said in the previous section KNNBasic is an algorithm that estimates the rating based completely in the k-nearest neighbors (depending in the Similarity measure in this case the used is [Mean Squared Difference](https://www.statisticshowto.datasciencecentral.com/mean-squared-error/)), Once the k-neighboors are determinated, The rating (<img src="https://latex.codecogs.com/gif.latex?\hat{r}_{ui}" />) is predicted as follows:

<p align="center">
  <img src="https://latex.codecogs.com/gif.latex?\hat{r}_{ui}&space;=&space;\frac{\sum_{v&space;\in&space;N_{i}^{k}(u)}&space;sim(u,v)&space;\cdot&space;r_{vi}}{\sum_{v&space;\in&space;N_{i}^{k}(u)}&space;sim(u,v)}"/>
</p>

Where <img src="https://latex.codecogs.com/gif.latex?N^{k}_{i}(u)"/> is the set of the k neighbors that have rated the item i.
<img src="https://latex.codecogs.com/gif.latex?sim(u,v)" /> is the Similarity measure between u,v choosen and <img src="https://latex.codecogs.com/gif.latex?r_{vi}" /> is the rating of the user v over the item i. 

2. <b> Assumptions </b>: This algorithm assumes that similar things exist in close proximity i.e that users having evaluated ratings over items similarly are users similar or have the same "taste" about the items.
3. <b>Pros and Cons </b>
	* Pros: Better predictions than "NormalPredictor",non-parametric.
	* Cons: Performance linked to variability and slow in contrast of "NormalPredictor" and Co-clustering. 

### KNNWithMeans

1. <b> Overall mathematical description </b>: This case is similar to the previous algorithm, but in addition is added the mean rating to the step 4 ( i.e how we predict the ratings as of the k nearest neighbors) in the next way:

<p align="center">
  <img src="https://latex.codecogs.com/gif.latex?\hat{r}_{ui}&space;=&space;\mu_{u}&space;&plus;&space;\frac{\sum_{v&space;\in&space;N_{i}^{k}(u)}&space;sim(u,v)&space;\cdot&space;(r_{vi}-\mu_{v})}{\sum_{v&space;\in&space;N_{i}^{k}(u)}&space;sim(u,v)}"/>
</p>

Where <img src="https://latex.codecogs.com/gif.latex?\mu_{x}}"/> is the mean of all ratings given by user x. the remaining terminology is analogous to the KNNBasic

2. <b> Assumptions </b>: This algorithm assumes that similar things exist in close proximity i.e that users having evaluated over items similarly are similar users or have the same "taste" about the items. In addition assumes the mean-rating of users is enough relevant to be considered.
3. <b>Pros and Cons </b>
	* Pros: Better predictions than "NormalPredictor",non-parametric, More information than KKBasic.
	* Cons: Performance linked to variability and slow in contrast of "NormalPredictor" and Co-clustering.
	
### KNNWithZScore

1. <b> Overall mathematical description </b>: Finally for this one is used the z-score of user, so is the most complete between the KNN-algorithms, the rating is predicted in the following manner:

<p align="center">
  <img src="https://latex.codecogs.com/gif.latex?\hat{r}_{ui}&space;=&space;\mu_{u}&space;&plus;&space;\sigma_{u}\frac{\sum_{v&space;\in&space;N_{i}^{k}(u)}&space;sim(u,v)&space;\cdot&space;(r_{vi}-\mu_{v})/\sigma_{v}}{\sum_{v&space;\in&space;N_{i}^{k}(u)}&space;sim(u,v)}"/>
</p>

Where <img src="https://latex.codecogs.com/gif.latex?\sigma_{x}" /> is the standard deviation of all ratings given by user x. The remaining terminology is analogous to the KNNWithMeans.

2. <b> Assumptions </b>: This algorithm assumes that similar things exist in close proximity i.e that users having evaluated over items similarly are similar users or have the same "taste" about the items. In addition assumes the z-score normalization of users is enough relevant to be considered.
3. <b>Pros and Cons </b>
	* Pros: Better predictions than "NormalPredictor",non-parametric and most complete KNN-algorithm, Can be modified in real-time .
	* Cons: Performance linked to variability and slow in contrast of "NormalPredictor" and Co-clustering. 
	
<br/><br/>
	
### Co-clustering

1. <b> Overall mathematical description </b>: Co-clustering (or simultaneous clustering ) prediction algorithm is a prediction algorithm que make use of the co-clustering technique over utems and items, i.e All the rating predictions are made over a cluster of similar users AND similar items: The co-cluster can be viewed as users with similar item likes or items liked by similar users ( In other words the lecture can be done in both directions). The rating are predicted as follows:

<p align="center">
  <img src="https://latex.codecogs.com/gif.latex?\hat{r}_{ui}=\bar{C}_{ui}&plus;(\mu_{u}-\bar{C}_{u})&plus;(\mu_{i}-\bar{C}_{i})"/>
</p>

Where <img src="https://latex.codecogs.com/gif.latex?\bar{C}_{ui}" /> is the average rating of co-cluster <img src="https://latex.codecogs.com/gif.latex?C_{ui}" />, <img src="https://latex.codecogs.com/gif.latex?\bar{C}_{u}" /> is the average rating of user-u’s cluster, and <img src="https://latex.codecogs.com/gif.latex?\bar{C}_{i}" /> is the average rating of item-i’s cluster. If the user is new (hasn't rated anything), the prediction is <img src="https://latex.codecogs.com/gif.latex?\hat{r}_{ui}=\mu_{i}" />. If the item is new, the prediction is <img src="https://latex.codecogs.com/gif.latex?\hat{r}_{ui}=\mu_{u}" />. If both the user and the item are new, the prediction is <img src="https://latex.codecogs.com/gif.latex?\hat{r}_{ui}=\mu" />. Consequently <img src="https://latex.codecogs.com/gif.latex?\mu_{u}" />,<img src="https://latex.codecogs.com/gif.latex?\mu_{i}" /> and <img src="https://latex.codecogs.com/gif.latex?\mu" /> are the mean of all ratings given by user u, the mean of all ratings given to item i and the mean of all ratings respectively.

The clusters are choosen to be the solution of the next least-square optimization problem:

<p align="center">
  <img src="https://latex.codecogs.com/gif.latex?\min_{C_{ui},C_{u},C_{i}}\sum_{i=1}^{m}\sum_{j=1}^{n}W_{ij}(r_{ij}-\hat{r}_{ij})" />
</p>

Where <img src="https://latex.codecogs.com/gif.latex?W_{ij}" /> is a parameter that indicates that rating exist, In summary
that the approximation matrix is the least squares solution that preserves the user, item and
co-cluster averages



2. <b> Assumptions </b>: Assumes that similar users and items, are in close proximity (like KNN).
3. <b>Pros and Cons </b>
	* Pros: Scalability and Computational efficiency and Acurateness.
	* Cons: Hardest predictor, Cold-start problem.
	
<br/><br/>
	
### Slope One

1. <b> Overall mathematical description </b>: Like the name indicates, the Slope one predictor algorithm, is a predictor of the form 
f(x)=x+b, which principle is based in the "<ins>Popularity difference</ins>" , this term refers to the case when one item is better liked than another item. This could be measured for example with the average difference of rating between this two items, the same difference could be used to predict ratings, assuming this difference is the expected difference between the user's of interests rating over this two items, resulting in a linear predictor. The predict rating is calculated as follows:

<p align="center">
  <img src="https://latex.codecogs.com/gif.latex?\hat{r}&space;_{ui}=\mu_{u}&plus;\frac{1}{|R_{i}(u)|}\sum_{j&space;\in&space;R_{i}(u)}&space;dev(i,j)"/>
</p>

Where <img src="https://latex.codecogs.com/gif.latex?\hat{r}_{ui}" /> Is the predicted rating, <img src="https://latex.codecogs.com/gif.latex?\mu_{u}" /> is the mean of all ratings given by user u,<img src="https://latex.codecogs.com/gif.latex?R_{ij}" /> is the set of relevant items, i.e. the set of items j rated by u that also have at least one common user with i and <img src="https://latex.codecogs.com/gif.latex?dev(i,j)" /> is defined as the average difference between the ratings of i and those of j:


<p align="center">
  <img src="https://latex.codecogs.com/gif.latex?dev(i,j)=&space;\frac{1}{|U_{ij}|}\sum_{u&space;\in&space;U_{ij}}r_{ui}-r_{uj}"/>
</p>

2. <b> Assumptions </b>: This algorithm assume that the predictor or approximate function best suited to the rating behavior is linear.
3. <b>Pros and Cons </b>
	* Pros: Very decent predictions,non-parametric, Easy to implement and Fast .
	* Cons: In this algorithm the number of ratings is not considered, this could induce bad predictions. 
