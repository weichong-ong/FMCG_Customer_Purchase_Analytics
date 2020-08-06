# Customer Analytics and Purchase Analytics Project Overview

Customer Analytics: I performed customer segmentation to gain insight into the purchase behavior using K-means clustering techniques combined with principal components analysis to reduce the dimensionality of the problem. 

Purchase Analytics: I carried out descriptive and predictive analysis of the purchase behaviour of customers, including price elasticity modeling for purchase probablity, brand choice (own brand and cross brand effects), and purchase quantity.

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
#### Price Elasticity of Purchase Probability
I used binomial logistic regression model to determine the probability of purchase where the dependant variable is based on the average price of chocolate candy bars. Furthermore, I calculated the price elasticity of purchase probability by segment as well as analyzed the influence of promotion activities.

E = beta * price * (1-Pr(purchase)) 
* |E|<1: inelastic -> increase price
* |E|>1: elastic -> decrease price

<p float="left">
  <img src="Price_Elasticity_of_Purchase_Probability" width="470" />
  <img src="Price Elasticity of purchase probability with and without promotion" width="470" />
</p>

#### Price Elasticity of Brand Choice Probability
I applied multinomial logistic regression model to predict brand choice probability based on the prices for the five brands. Additionally, I compared own price brand choice elasticity with cross price brand choice elasticity by customer segments.

E = -beta(own price) * price(cross brand) * Pr(cross brand)
* E(cross brand) > 0   -> Brands are substitutes for one another
* |E(cross brand)| > |E(own brand)|   -> The alternative brand is considered a strong substitute

<p float="left">
  <img src="Own and cross price elasticities by customer segments" width="470" />
</p>

#### Price Elasticity of Purchase Quantity / Price Elasticity of Demand
I implemented multiple linear regression model to predict the purchase quantity by price and promotion features in the model. Lastly, I calculated the price elasticity of purchase quantity with and without active promotional activities for each price point.

E = beta * price / quantity(purchase)
<p float="left">
  <img src="Price_Elasticity_of_Purchase_Quantity_with_and_without_Promotion" width="470" />
</p>
