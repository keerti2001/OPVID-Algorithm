# OPVID-Algorithm
Outlier Probability via Intrinsic Dimension

Intrinsic Dimension of a Data Set

A central concept of data mining and machine learning is that of comparing data. That is, given some dataset, we want to analyse its properties and use this analysis to create a predictive model of how it will change over time, or simply compare it to other existing data sets to see their similarities. The effectiveness of these types of predictive and comparison algorithms depend on the nature of the descriptive information gathered from the data sets. The amount of these features that are distilled from the data can vary greatly and the cardinality is usually referred to as the dimensionality of the data.

Calculation of ID Score

Suppose we have data points contained in a vector space which is equipped with a distance measure (e.g. the Euclidean norm). The distances from each point to some fixed query point q will all be positive numbers and thus a variable which takes on any such distance can be represented as a (continuous) random variable X. Since X is a (continuous) random variable, we have an associated probability density function fX(x) which describes the probability that the variable will be a certain value and additionally, the cumulative density function FX(x):= P(X<= q) which describes the probability that X will take a value less than or equal to q. 


Remarkably, if we have clustered data in a d-dimensional subspace of an n-dimensional vector space then the continuous ID is equal to the dimension of the cluster, d. For the purposes of this paper, it suffices to say that various methods of estimating the (local/continuous) ID of a data set exist and usually depend on a k-nearest neighbour parameter to compare local distances of points to one another. We call such a parameter the context set k and denote it kc. For clarity we provide one particular approximation to make the application of the Eq. (1) more concrete. Let q be the query point whose ID score we wish to determine. Set kc = 10 such that we want to approximate the points ID score relative to its 10-nearest-neighbours and let x1,x2, …. X10 denote the (increasing) ordered distances from the point q to its 10-nearest-neighbours.

 

Application to Outlier Detection

The insight that the (continuous) ID score of a point q is equal to the dimension of the cluster it belongs to and increases if the point lies outside a cluster was a central motivation behind the Intrinsic Dimensionality Outlier Score (IDOS). 

where kr >= 1 such that Nkr (q) is the set of kr-nearest neighbours of the query point q and ID (p) is the IDScore (see for example the estimator given by Eq. (2)) of the point p. Similar to the LOF score, we say that a point q is an outlier if IDOS (q) >> 1 and an inlier if IDOS (q) is almost equal to 1.
The IDOS algorithm is insufficient due to the fact that we want to run such an outlier detection algorithm for tens of thousands of different data sets and for each data set the notion of an outlier score much greater than 1" varies. That is, for one particular telemetry data set, an outlier score for a query point q may correspond to an outlier if its score is 5, whereas for another telemetry data set, a value of 15 may only indicate that the point is truly an outlier. These differences imply we must have a normalized outlier score such that we will always know whether a point has a high likelihood of being an outlier for any given data set.

 	In light of these considerations we propose a new outlier score, the Outlier Probability via Intrinsic Dimension (OPVID) score, which serves exactly this purpose. The general outline is as follows and makes use of a normalization technique used to obtain the probability measure.

After determining the ID score of every point in the data, we determine the difference between a points own ID score and the average of its local kr-nearest neighbours ID scores.

Which we call the Probabilistic Intrinsic Dimension Outlier Score (PIDOS) and will be close to zero for points which belong to clusters. As a side remark, we note that this score is not a probability score yet since it clearly can be negative. Now, using the set of all PIDOS scores we can define the Outlier Probability via Intrinsic Dimension score of a query point q.
 
Where    a scaling factor, PIDOSSTD (q) is the standard deviation of the PIDOS scores of the query points local kr-nearest neighbours, and erf is the Gaussian error function. We note that the application of the Gaussian error function assumes that the PIDOS scores are normally distributed around zero, which, for points which have an ID score close to the average of its neighbours is a just assumption. Therefore, the OPVID score for a point which belongs to a local cluster and hence has each of its neighbours sharing a close ID score will be close to zero whereas a point which strays outside of a local cluster will have a score closer to one.
