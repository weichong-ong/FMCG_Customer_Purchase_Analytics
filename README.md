# Customer Analytics and Purchase Analytics Project Overview

Make sure all the files in the local disk are up-to-date: (pull all the file from master)
		git pull

Every time starts a new task: create new branch for this particular task (instead of push all the file to master)
		git checkout -b branch_name

git add .
git commit -m “comments”
git push (git push —set-upstream origin branch_name)

Customer Analytics: The first part of the course focuses on how to perform customer segmentation, using a hands-on approach. It involves the application of hierarchical and flat clustering techniques for dividing customers into groups. It also features applying the Principal Components Analysis (PCA) to reduce the dimensionality of the problem, as well as combining PCA and K-means for an even more professional customer segmentation.

Purchase Analytics: The second part of the course explores both the descriptive and predictive analysis of the purchase behaviour of customers, including models for purchase incidence, brand choice, and purchase quantity. Not only that, but it also covers the application of state-of-the-art deep learning techniques to make predictions using real-world data.

* Standardizing data, so that all features have equal weight.
* Dividing a population of customers into groups that share similar characteristics using K-means clustering techniques combined with principal components analysis
* Grouping the customer by segments to gain insight into the purchase behavior

## Code and Resources used
**Python Version:** 3.8   
**Packages:** pandas, numpy, sklearn, scipy, matplotlib, seaborn, pickle    
**Modules:** dendrogram, linkage, KMeans, PCA

## Customer Analytics
### Exploration Data Analysis
Customer data features: 2000 Obeservations
* Sex
* Marital status
* Age
* Education
* Income
* Occupation
* Settlement Size

### Visualization
Pearson correlation method (linear dependency between variables) was used to explore how the variables correlate, in order to get an initial understanding of the relationship between them 
* There is a strong positive correlation between age and education of a value of 0.65 and between income and occupation of a value of 0.68
![alt text]()

### Customer segmentation
#### Data Preprocessing - Standardization
Standardizing data using StandardScaler, so that all features have equal weight as I didn't wanted to create bias due to the large values of 'Income'.
* StandardScaler removes the mean and scales each feature/variable to unit variance. This operation is performed feature-wise in an independent way.
* StandardScaler can be influenced by outliers (if they exist in the dataset) since it involves the estimation of the empirical mean and standard deviation of each feature.
#### Cluster Analysis - K-means
#### Dimensionality Reduction - PCA

## Purchase Analytics
### Descriptive analysis

### Elasticity Modeling
#### Price Elasticity of Purchase Probability
#### Price Elasticity of Brand Choice Probability
#### Price Elasticity of Purchase Quantity
