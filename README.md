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

Purchase Analytics: The second part of the course explores both the descriptive and predictive analysis of the purchase behaviour of customers, including models for purchase incidence, brand choice, and purchase quantity.

* Standardizing data, so that all features have equal weight.
* Dividing a population of customers into groups that share similar characteristics using K-means clustering techniques combined with principal components analysis
* Grouping the customer by segments to gain insight into the purchase behavior

## Code and Resources used
**Python Version:** 3.8   
**Packages:** pandas, numpy, sklearn, matplotlib, seaborn, pickle     
**Modules:** StandardScaler, KMeans, PCA, LogisticRegression, LinearRegression  
**Datasets (~15000 rows):** Udemy course - Customer Analytics in Python 2020

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
#### Price Elasticity of Purchase Probability (Binomial Logistic Regression)
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
Insert 'Price_Elasticity_of_Purchase_Probability' picture here

Career focused segment: 
* smaller coefficient -> this segment is less elastic than the average customer
* At 1.39 price point, they become inelastic, which is 14 cents higher than the average turning point.
* Increase prices if in the 0.5-1.39 range
Fewer oppurnities segment: 
* This segment is more price sensitive compared to the average and a lot more sensitive compared to the career focused.
* The line is much steeper. This means that with an increase in price, they become more and more elastic much faster.
* The tipping point between elasticity and inelasticity stands at 1.27. Compared to the average tipping pint (1.25), it seems that this segment is more inelastic at lower prices
* Two main reasons:
* Theory 1: abundance of data results in a better model
* Theory 2: This segment enjoys candy bars so much that a price increase in the lowe price range doesn't affect them. However, once it starts becoming expensive, it does not make any financial sense to them to invest in it
* These results confirm in a way what we've observed during the descriptive analysis of the data. Additionally, we've obtained exact values of how purchase probability changes with the change in price
![alt text](https://github.com/Wei-Chong-Eden/Customer_Purchase_Analytics/blob/Customer_Analytics/DA_Brand_Choice.png)

* The well-off segment are the least elastic when compared to the rest, so, their purchase probability elasticity is not as affected by price.
* The price elasticities for the Standard segment seem to differ across price range. This may be due to the fact that the standard segment is least homogenous, which we discovered during our descriptive analysis. It may be that the customers in this segment have different shopping habbits, which is why their customers start with being more elastic than average but then shift to being more inelastic than the average customer  

Insert 'Price Elasticity of purchase probability with and without promotion' picture here
* Customers are less price sensitive to price changes when there are promotion activities
#### Price Elasticity of Brand Choice Probability (Multinomial Logistic Regression)
* Coef_Brand_1: The more the price of a competitor increases, the higher the probability of customers switching to our own brand would be, except Price_5. There is a positive relationship between our own brands purchase probability and a competitive brand increasing their price 
* Own brand effects and Cross brand effects: A marketing mix tool of our brand reflects not only the choice probability for that brand but the choice probabilities for all other brands as well.
* What would happen to the purchase probability of brand 5 if a competitor changed their pricing? Compared with the brand with the closest price (Cross Price Elasticity)
E = -beta(own price) * price(cross brand) * Pr(cross brand)
* This indicates that if competitor brand 4 increases prices, the purchase probability for our own brand would increase. Elasticity show us exactly how much more. 
* E(cross brand) > 0   -> Brands are substitutes for one another
* |E(cross brand)| > |E(own brand)|   -> The alternative brand is considered a strong substitute (Brand 4 is a strong substitute for brand 5 for all price up to 1.65)
* However, price range of brand 4 is between 1.76 and 2.26. At this price range, the elasticity is positive. Brand 5 purchase probability still increases with the increase in price of brand 4, but at a slower rate.
* We can conclude that when it comes to the average customer, brand 4 is an albeit weak substitute for brand 5. In light of these results, brand 5 can create a marketing strategy for targeting customers which choose brand 4 and attract them to buy the own brand. However, targeting the average customer can be a laboursome task. No brand can make everyone happy but a brand can make a certain customer segement happy -> Own and cross price elasticities by customer segments  
Insert pic here  
Brand choice analysis:
* Standard customer is more elastic when compared to the average. The difference becomes even more pronounced when compared the standards to career focused and well-off segment in the price range 2.1-2.8. The elasticity of the standard segment is between -1.42 and -2.7. Therefore, its purchase probability for the own brand is elastic for the entire observed price range of the brand. If we were to win some of the standard segment market, our marketing strategy would be to lower prices in this price range to increase the purchase probability for this segment. However, this segment isn't homogenous and a marketing strategy based on only this segment might not be in the best interest
* Career focused customers are the least elastic among the rest. They are inelastic throughout the whole price range. It means this segment is not really affected by the increase in price of the own brand. In addtion, their cross price elasticity also has extremely low values. This shows that they are unlikely to switch to the competitor brand. The marketing team could increase prices of our own brand without fear of losing too much market share.
* The own price elasticity of the fewer opportunities segment has a more pronounced shape. This segment is inelastic at lower price point but rapidly becomes the most elastic customers at higher prices. It is important to notice that this segment almost never buys brand 5 or brand 4. Less than 1 percent of their customers have purchased one of thes brands. Therefore, there were not enough observations to obtain an accurate model and that is the reason why both curves look so out of character. In order for marketing to target this segment in particular brand 5, more data of purchases from this segment is needed. However, these people might be simply not the target group as brand 5 may be too pricey for this segment and more data may never be obtained
* It appears that career focused and well-off segments require the most attention as they are actually the people that purchase brand 5
* The well-off segment is much more elastic than the career focused. Therefore, if we were to increase our prices, this would barely affect the career focused but would seriously damage our well-off segment sales.
* If brand4 were to decrease their price, it would affect the well-off segment but not the career focused. Therefore, a tiny decrease in our pricing would compensate such competitor move. This is extremely important to know because if prices of chocolate candy bars were to drop, we would have space to decrease our price offering while gaining solid market share from the well-off segment and practically retaining our career focused customer base.
#### Price Elasticity of Purchase Quantity (Multiple Linear Regression)
E = beta * price / Quantity(purchase)
* Customers are a tiny bit more elastic when there is a promotion. However, overall customers are inelastic towards purchase quantity for all prices from 0.5-2.7
* The two lines practically overlap at many of the price points. The reason might be that the variables we included in our model hold no predictive value. Therefore, it might seem like it doesn't really make sense to focus too much on the purchase quantity. Neither price nor promotions shifts appear to affect the customer decisions.
* Alternatively, calculate price elasticity of purchase quantity for each brand. 
Insert pic 'Price Elasticity of Purchase Quantity with Promotion'
