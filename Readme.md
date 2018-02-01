### Matrix Factorization for Recommendation: An Implementation using Netflix data.

This is a project in the framework of the course *Advances in Data Mining* of Leiden University. 

#### Introduction

Recommendation systems are software tools and techniques [1] used in order to filter massive amounts of information [2] and recommend specific products or items to users that are highly likely to like, and therefore give a high rating. Thus, they are utilized by many commercial areas including, but not limited to movies, news, books, music etc. Many different methods exist for constructing a recommender system such as naive approaches, in which the system calculates the average rating of an item as rated by different users, or calculates the average rating of the items by the same user, and then recommends an item that has a relatively high average rating. In more advanced methods such as collaborative filtering [1], [2], [3], [4], [5], the same items are recommended to "similar" users, these are users that tend to like the same items, and have common preferences. Another approach, called content based approach [1], [2], [3], [6], items are recommended to a user because he/she liked similar items in the past. Finally, other approaches include matrix factorization such as, for example, Singular Value Decomposition [7], [8].

#### Matrix Factorization

This project is a Python implementation of the Matrix Factorization technique described in []. In the matrix factorization approach, the goal is to estimate matrix <a href="https://www.codecogs.com/eqnedit.php?latex=X&space;\in&space;\mathbb{R}^{I\times&space;J}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?X&space;\in&space;\mathbb{R}^{I\times&space;J}" title="X \in \mathbb{R}^{I\times J}" /></a> containing the ratings given by a user <a href="https://www.codecogs.com/eqnedit.php?latex=i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?i" title="i" /></a> to a movie <a href="https://www.codecogs.com/eqnedit.php?latex=j" target="_blank"><img src="https://latex.codecogs.com/gif.latex?j" title="j" /></a>, using a matrix decomposition method, called Singular Value Decomposition (SVD). Using SVD, the approximation of matrix <a href="https://www.codecogs.com/eqnedit.php?latex=X" target="_blank"><img src="https://latex.codecogs.com/gif.latex?X" title="X" /></a> can be written as a product of two matrices, namely <img src="https://latex.codecogs.com/gif.latex?\hspace{1&space;mm}&space;U&space;\in&space;\mathbb{R}^{I&space;\times&space;K}" title="\hspace{1 mm} U \in \mathbb{R}^{I \times K}" />, and <a href="https://www.codecogs.com/eqnedit.php?latex=M&space;\in&space;\mathbb{R}^{K&space;\times&space;J}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?M&space;\in&space;\mathbb{R}^{K&space;\times&space;J}" title="M \in \mathbb{R}^{K \times J}" /></a>, that is <a href="https://www.codecogs.com/eqnedit.php?latex=X\simeq&space;U\cdot&space;M" target="_blank"><img src="https://latex.codecogs.com/gif.latex?X\simeq&space;U\cdot&space;M" title="X\simeq U\cdot M" /></a>. Matrices <a href="https://www.codecogs.com/eqnedit.php?latex=U" target="_blank"><img src="https://latex.codecogs.com/gif.latex?U" title="U" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=M" target="_blank"><img src="https://latex.codecogs.com/gif.latex?M" title="M" /></a> contain <a href="https://www.codecogs.com/eqnedit.php?latex=k" target="_blank"><img src="https://latex.codecogs.com/gif.latex?k" title="k" /></a> features for each user and movie. For example, a feature of matrix <a href="https://www.codecogs.com/eqnedit.php?latex=U" target="_blank"><img src="https://latex.codecogs.com/gif.latex?U" title="U" /></a> could be how much a specific user <a href="https://www.codecogs.com/eqnedit.php?latex=i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?i" title="i" /></a> likes action movies, and the corresponding feature of matrix <a href="https://www.codecogs.com/eqnedit.php?latex=M" target="_blank"><img src="https://latex.codecogs.com/gif.latex?M" title="M" /></a> could be how much a specific movie <a href="https://www.codecogs.com/eqnedit.php?latex=j" target="_blank"><img src="https://latex.codecogs.com/gif.latex?j" title="j" /></a> is considered to be an action movie. The dot product of all these different feature vectors for each available combination of user and movie yields our estimate of the rating a user <a href="https://www.codecogs.com/eqnedit.php?latex=i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?i" title="i" /></a> would give to the movie <a href="https://www.codecogs.com/eqnedit.php?latex=j" target="_blank"><img src="https://latex.codecogs.com/gif.latex?j" title="j" /></a>. High values of both these two feature vectors yield higher ratings, whereas the opposite is true for small values in both of these two feature vectors. It should be noted that we do not actually know what these feature vectors represent. The goal is to find the values of these vectors that best represent/estimate matrix <a href="https://www.codecogs.com/eqnedit.php?latex=X" target="_blank"><img src="https://latex.codecogs.com/gif.latex?X" title="X" /></a>, without knowing the actual meaning of them.

#### Data

We use the *MovieLens 1M* data set which can be found (here)[http://grouplens.org/datasets/movielens/]. The data set contains about 1.000.000 ratings given to about 4.000 movies by about 6.000 users. Additionally, some information is provided about movies (genre, title, production year) and users (gender, age, occupation). 

#### Function

The function **MatrixFactorization()** takes several arguments, specifically:     

* **data** (*string*): Directory of the data on which the technique is applied.    
* **delimiter** (*string*), *Default* **None**: Delimiter symbol to split the columns of the data.     
* **useCols** (*tuple*), *Default* **None**: Columns to be chosen from the data set, in order to apply the technique. In the case of Netflix data, these columns would be `user_id`, `movie_id`, `rating`.     
* **dtype** (*string*), *Default* **None**: Type of the data in columns (for example 'int').     
* **method** (*string*), *Default* **None**: Whether to perform Cross Validation (CV). Input 'cv' to perfrom CV.    
* **percTrain** (*float*), *Default* **None**: Percent of train set, in case no CV is performed.    
* **numFolds** (*int*), *Default* **None**: Number of folds for CV.    
* **log** (*boolean*), *Default* **True**: Whether to print an informative log.    
* **logIteration** (*boolean*), *Default* **True**: Whether to print an informative log in each iteration.
* **seed** (*int*), *Default* **100**: Seed for reproducibility of results.
* **learningRate** (*float*), *Default* **0.005**: The learning rate.
* **lambdaReg** (*float*), *Default* **0.05**: Regularization parameter to avoid overfitting.    
* **numFeatures** (*int*), *Default* **10**: The number of features for users and movies.    
* **iterations** (*int*), *Default* **75**: The number of iterations the algorithm should perform.


