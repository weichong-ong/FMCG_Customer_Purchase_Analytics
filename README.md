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

## Customer Analytics - Segmentation
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

![alt text](https://github.com/Wei-Chong-Eden/Customer_Purchase_Analytics/blob/Customer_Analytics/CS_Kmeans.png)

#### Dimensionality Reduction - PCA
Three components was chosen as I wanted to keep around 80 % of the explained variance  
* There is a positive correlation between component 1 and age, income, occupation and settlement size. Thus, this component shows the career focus of the individual. 
* Component 2 doesn't refer to the career but rather to an individual's education and lifestyle.
* Age, marital status and occupations are the most important determinants in the component 3. These indicate the work experience and life experience.

![alt text](https://github.com/Wei-Chong-Eden/Customer_Purchase_Analytics/blob/Customer_Analytics/CS_PCA.png)

#### K-means clustering with PCA
I fitted K-means using the PCA scores and created a K-means-PCA-model with 4 clusters.

Results:
* 'well-off' segment is highest on all three components (1:career, 2:education and lifestyle and 3:experience)  
* 'fewer-opportunities' segment: the lowest average PCA scores for 1:career, 2:education and lifestyle but high on 3:experience  
* 'career-focused' segment: high PCA scores for 1:career, but low for 2:education and lifestyle, independent from 3:experience  
* 'standard' segment: low 1:career and 3:experience while normal to high 2:education and lifestyle  

The division of the segments based on the components is much more pronounced with the help of PCA by reducing the number of variables by combining them into bigger, more meaningful features.  

![alt text](https://github.com/Wei-Chong-Eden/Customer_Purchase_Analytics/blob/Customer_Analytics/CS_Kmeans_PCA.png)

## Purchase Analytics - Positioning
Sales promotions: Merchandising, price reduction, display and feature  
### Data Preprocessing
* I applied the segmentation model (scaler.pickle, pca.pickle, kmeans_pca.pickle) to the new dataset (purchase_data.csv) in order to place new customers into clusters.  

### Descriptive analysis
* Grouped the data by individual and then by segments to gain insight into customer shopping habits.
* Identified how often each segment group go shopping, how much money they spend and what products they purchase.
* I displayed the standard deviation as a straight line. The bigger the length, the higher the standard deviation is.

  * Total number of visits for each segment 
  * Total number of purchases for each segment 
  * Brand choice for each segment 
  * Revenue for each brand for each segment

![alt text](https://github.com/Wei-Chong-Eden/Customer_Purchase_Analytics/blob/Customer_Analytics/DA_Num_Visits.png)
![alt text](https://github.com/Wei-Chong-Eden/Customer_Purchase_Analytics/blob/Customer_Analytics/DA_Num_Purchases.png)

* The 'career-focused' segment visits the store and buy products most ofthen. However the standard deviation amongst customers is the highest. This implies that the customers in this segment are at least homogenous, that is least alike when it comes to how often they visit the grocery store and buy products. 
* The most homogenous segments appears to be that of the 'fewer-opportunities' segment.

![alt text](https://github.com/Wei-Chong-Eden/Customer_Purchase_Analytics/blob/Customer_Analytics/DA_Brand_Choice.png)
* The five beands are arranged in ascending order of price
* Almost 70% of the 'fewer-opportunities' segment chooses Brand_2 chocolate
* 63% of the 'career-focused' segment buys Brand_5 chocolate which is the most expensive brand. This indicates that people of this segment is looking for some kind of luxury status. This may be an opportunity to raise the price of Brand_5 even further
* The price of the chocolate bars isn't waht matters the most to the customers
* The 'standard' segment is the most heterogeneous segment. Try to influence them to try different brands might be a good idea in order to gain actaionable insignt.

![alt text](https://github.com/Wei-Chong-Eden/Customer_Purchase_Analytics/blob/Customer_Analytics/DA_Revenue.png)
* Apparently even though 'career focused' segment is the second largest, it brings the highest revenue. It seems that they are by far the most prominent segment for the store with regard to chocolate candy bars.
* The standard is almost equal in size but it brings less than half that revenue.
* The 'well-off' and the 'fewer-opportunities' segments spend around the same amount of money on chocolate candy bars with the note that the latter is twice the size of the former. 
* Possible marketing strategies:
  * If Brand_3 reduces its price, 'standard' segment could pivot towards it.
  * Brand_4 could try cautiously increasing its price as 'well-off' segment seem to be loyal to this brand and not really affected by price. Most of the customers could be retained and reveneu per sale could be increased.

### Elasticity Modeling
Price Elasticity, E = % Change in economic outcome of interest (Units sold) / 1% change in price  
E = Y%/P%
#### Price Elasticity of Purchase Probability
E = delta(Pr(purchase))/Pr(purchase) / delta(price)/price  
E = beta * price * (1-Pr(purchase)) 
* The decrease in price is slow in the range between 0.5 to 1.1 and then it becomes steeper after the 1.1 mark  
* The price elasticities are all negative because the model price coefficient is negative with -2.35. It indicates the inverse proportionality between price and purchase probability  
* If the percent change in price is greater than 100%, the purchase probability is elastic. For changes less than 100%, it is inelastic (inelastic: |E|<1)
* 1.10 point: For each increase in price by 1%, the probability of purchase will decrease by -0.69%
* The important observation here is that an increase of 1% in elasticity leads to a decrease of less than 1%. Therefore, purchase probability at this point is inelastic. 
* 1.50 point: The elasticity is -1.7. An increase of 1% in price would translate into a decline of -1.7% of purchase probability. Therefore, an increase of 1% will lead to a decrease of almost 2% in purchase probabillity. In this case, purchas probability is elastic.
* For inelastic values, we increase price as it wouldn't cause a significant decrease in purcahse probability
* For elastic values, we decrease price
* In the graph, it starts from being inelastic and then swiches to being elastic. This happens at the 1.25 price point.
* Conclusion: With the prices lower than 1.25, we can increase our product price without losing too much in terms of purchase probability. For prices higher than 1.25, we have more to gain by reducing our price.

Purchase elasticities by segments
#### Price Elasticity of Brand Choice Probability
E = -beta(own price) * price(cross brand) * Pr(cross brand)
#### Price Elasticity of Purchase Quantity
E = beta * price / Quantity(purchase)
