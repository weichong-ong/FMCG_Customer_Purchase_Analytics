# Customer Analytics and Purchase Analytics Project Overview
Customer Analytics: The first part of the course focuses on how to perform customer segmentation, using a hands-on approach. It involves the application of hierarchical and flat clustering techniques for dividing customers into groups. It also features applying the Principal Components Analysis (PCA) to reduce the dimensionality of the problem, as well as combining PCA and K-means for an even more professional customer segmentation.

Purchase Analytics: The second part of the course explores both the descriptive and predictive analysis of the purchase behaviour of customers, including models for purchase incidence, brand choice, and purchase quantity. Not only that, but it also covers the application of state-of-the-art deep learning techniques to make predictions using real-world data.

* Standardizing data, so that all features have equal weight.
* Dividing a population of customers into groups that share similar characteristics using K-means clustering techniques combined with principal components analysis
* Grouping the customer by segments to gain insight into the purchase behavior

## Code and Resources used
Python Version: 
Packages: pandas, numpy, sklearn, scipy, matplotlib, seaborn, pickle

## Customer Analytics
### Exploration Data Analysis
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
