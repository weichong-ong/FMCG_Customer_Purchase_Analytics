# Customer Analytics and Purchase Analytics Project Overview

* Make sure all the files in the local disk are up-to-date: (pull all the file from master or other branch)
  * git pull

* Every time starts a new task: create new branch for this particular task (instead of push all the file to master)
  * git checkout -b branch_name

* Switch to this branch: 
  * git checkout Customer_Analytics
* git add .
* git commit -m “comments”
* git push (git push —set-upstream origin branch_name)

Customer Analytics: The first part of the course focuses on how to perform customer segmentation, using a hands-on approach. It involves the application of hierarchical and flat clustering techniques for dividing customers into groups. It also features applying the Principal Components Analysis (PCA) to reduce the dimensionality of the problem, as well as combining PCA and K-means for an even more professional customer segmentation.

Purchase Analytics: The second part of the course explores both the descriptive and predictive analysis of the purchase behaviour of customers, including models for purchase incidence, brand choice, and purchase quantity. Not only that, but it also covers the application of state-of-the-art deep learning techniques to make predictions using real-world data.

* Standardizing data, so that all features have equal weight.
* Dividing a population of customers into groups that share similar characteristics using K-means clustering techniques combined with principal components analysis
* Grouping the customer by segments to gain insight into the purchase behavior

## Code and Resources used
**Python Version:** 3.8   
**Packages:** pandas, numpy, sklearn, matplotlib, seaborn, pickle     
**Modules:** StandardScaler, KMeans, PCA

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

#### Visualization
Pearson correlation method (linear dependency between variables) was used to explore how the variables correlate, in order to get an initial understanding of the relationship between them.  
The first step to identifying similar consumers and putting them together in group.  
* There is a strong positive correlation between age and education of a value of 0.65, between income and occupation of a value of 0.68 and between occupation and settlement size of 0.57

![alt text](https://github.com/Wei-Chong-Eden/Customer_Purchase_Analytics/blob/Customer_Analytics/EDA_Corr_Map.png)

### Data Preprocessing
#### Standardization
Standardizing data using StandardScaler, so that all features have equal weight as I didn't wanted to create bias due to the large values of 'Income'.  
Transforming the features in such a way that their values fall within the same numerical range.  
* StandardScaler removes the mean and scales each feature/variable to unit variance. This operation is performed feature-wise in an independent way.
* StandardScaler can be influenced by outliers (if they exist in the dataset) since it involves the estimation of the empirical mean and standard deviation of each feature.
### Customer segmentation
#### Cluster Analysis - K-means
I calculated the within cluster sum of squares (WCSS) for each of the clustering solutions and used the WCSS values to determine the best clustering solution.  
k-means++ algorithm was used to find the best starting points for the centroid.  
Elbow method was used to determine the number of clusters.  

Results - four clusters:
* well-off: Oldest segment, more than 2/3 are in relationships, highest level of education and income, smallest segment    
* fewer-opportunities: Mostly single, people in thier thirties, relatively low education level and income, live in small cities  
* standard: Youngest segment, people in relationships, medium level of education, average income and middle management jobs, largest segment   
* career focused: Mostly men, less than 20% in relationships, relatively low education level, high income and occupation, majority live in big and middle size cities  

CS_Kmeans
![alt text]()

#### Dimensionality Reduction - PCA
Three components was chosen as I wanted to keep around 80 % of the explained variance  
* There is a positive correlation between component 1 and age, income, occupation and settlement size. Thus, this component shows the career focus of the individual. 
* Component 2 doesn't refer to the career but rather to an individual's education and lifestyle.
* Age, marital status and occupations are the most important determinants in the component 3. These indicate the work experience and life experience.

CS_PCA
![alt text]()

#### K-means clustering with PCA
I fitted K-means using the PCA scores and created a K-means-PCA-model with 4 clusters.

Results:
* 'well-off' segment is highest on all three components (1:career, 2:education and lifestyle and 3:experience)  
* 'fewer-opportunities' segment: the lowest average PCA scores for 1:career, 2:education and lifestyle but high on 3:experience  
* 'career-focused' segment: high PCA scores for 1:career, but low for 2:education and lifestyle, independent from 3:experience  
* 'standard' segment: low 1:career and 3:experience while normal to high 2:education and lifestyle  

The division of the segments based on the components is much more pronounced with the help of PCA by reducing the number of variables by combining them into bigger, more meaningful features.  
CS_Kmeans_PCA
![alt text]()

## Purchase Analytics
### Data Preprocessing
### Descriptive analysis

### Elasticity Modeling
#### Price Elasticity of Purchase Probability
#### Price Elasticity of Brand Choice Probability
#### Price Elasticity of Purchase Quantity
