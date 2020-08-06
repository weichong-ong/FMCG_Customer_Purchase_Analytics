# Customer Analytics and Purchase Analytics Project Overview

Customer Analytics: I performed customer segmentation to gain insight into the purchase behavior using K-means clustering techniques combined with principal components analysis to reduce the dimensionality of the problem. 

Purchase Analytics: I carried out descriptive and predictive analysis of the purchase behaviour of customers, including price elasticity modeling for purchase probablity, brand choice, and purchase quantity.

## Code and Resources used
**Python Version:** 3.8   
**Packages:** pandas, numpy, sklearn, matplotlib, seaborn, pickle     
**Modules:** StandardScaler, KMeans, PCA, LogisticRegression, LinearRegression  
**Datasets (~15000 rows):** Udemy course - Customer Analytics in Python 2020

## Customer Analytics - Segmentation
### Exploration Data Analysis
I used Pearson correlation method (linear dependency between variables) to explore how the variables correlate, in order to get an initial understanding of the relationship between them.  
<p float="left">
  <img src="ttps://github.com/Wei-Chong-Eden/Customer_Purchase_Analytics/blob/Customer_Analytics/EDA_Corr_Map.png" width="470" />
</p>

### Data Preprocessing
I standardized data using StandardScaler, so that all features have equal weight as I didn't wanted to create bias due to the large values of 'Income'.  
### Customer segmentation - K-means clustering with PCA
I fitted K-means using the PCA scores and created a K-means-PCA-model with 4 clusters.
* well-off 
* fewer-opportunities
* career-focused
* standard
<p float="left">
  <img src="https://github.com/Wei-Chong-Eden/Customer_Purchase_Analytics/blob/Customer_Analytics/CS_Kmeans_PCA.png" width="470" />
</p>

## Purchase Analytics - Positioning
### Data Preprocessing
* I applied the segmentation model (scaler.pickle, pca.pickle, kmeans_pca.pickle) to the new dataset (purchase_data.csv) in order to group new customers into clusters.  

### Descriptive analysis
* Grouped the data by individual and then by segments to gain insight into customer shopping habits.
* Identified how often each segment group go shopping, how much money they spend and what products they purchase.
* I displayed the standard deviation as a straight line. The bigger the length, the higher the standard deviation is.

<p float="left">
  <img src="https://github.com/Wei-Chong-Eden/Customer_Purchase_Analytics/blob/Customer_Analytics/DA_Num_Visits.png" width="470" />
  <img src="https://github.com/Wei-Chong-Eden/Customer_Purchase_Analytics/blob/Customer_Analytics/DA_Num_Purchases.png" width="470" /> 
</p>

<p float="left">
  <img src="https://github.com/Wei-Chong-Eden/Customer_Purchase_Analytics/blob/Customer_Analytics/DA_Brand_Choice.png" width="470" />
</p>

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
