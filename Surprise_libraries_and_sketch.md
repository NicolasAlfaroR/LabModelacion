## 3 surprise libraries chosen:

 * NormalPredictor: Predictor of rating, assuming a normal distribution of them.
     * Pros: Easiest predictor, intuitive and fast.
     * Cons: Worst predictions,  performance strongly linked to variability.

 * KNNWithMeans
     * Pros:Better predictions than "NormalPredictor",non-parametric.
     * Cons: Performance linked to variability and slow in contrast of "NormalPredictor" and Co-clustering. 

 * Co-clustering
     * Pros:Scalability and Computational efficiency.
     * Cons: Hardest predictor, tradeoff between scalability and accuracy .


*Sketch.

Once user-user filter was created , the final step would find ( for a specific user ) items that the user of interest, wasn't interacted before
for each n similar users, then sort in a descendant way this items, by mean rating. Finally recommend the first m items.

```bash
similar_users=TopN_Plural(df,n,Usuarios) #list of lists
Recommender_list=[]
for i in range(0,len(similar_users):
   for similar_user in similar_users[i]:
	.
	. #Finding the items fullfiling the previous characteristics, and storing them in a dictionary {ID_item:rating}
	.
   Recommend the top m items by ratings.
   #Store this list in Recommender_list
return (Recommender_list)

```
