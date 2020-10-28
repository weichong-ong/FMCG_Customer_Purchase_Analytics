# Customer Purchase Analytics Project Overview

## Part I: Customer Analytics - Segmentation
Performed customer segmentation to gain insight into the purchase behavior using K-means clustering techniques combined with principal components analysis to reduce the dimensionality of the problem.

<p align="center">
  <img src="/images/CS_Kmeans_PCA.png" width="600" />
</p>

## Part II: Purchase Analytics - Positioning
Carried out descriptive and predictive analysis of the purchase behaviour of customers, including price elasticity modeling for purchase probablity, brand choice (own brand and cross brand effects), and purchase quantity.
### Descriptive Analysis

<p align="center">
  <img src="/images/Pie_Chart_Segment_Proportion.png" width="600" />

### Predictive Analysis

<p align="center">
  <img src="/images/PA_Price_Elasticity_of_Purchase_Probability.png" width="600" />

## Code and Resources
**Python Version:** 3.8
**Packages:** pandas, numpy, sklearn, matplotlib, seaborn, pickle
**Modules:** StandardScaler, KMeans, PCA, LogisticRegression, LinearRegression
**Datasets (~60000 observations):** Udemy - Customer Analytics in Python 2020

## Customer Analytics - Segmentation
### Exploration Data Analysis
Used Pearson correlation method (linear dependency between variables) to explore how the variables correlate, in order to get an initial understanding of the relationship between them.

### Data Preprocessing
Standardized data using StandardScaler, so that all features have equal weight.
### Customer segmentation - K-means clustering with PCA
Fitted K-means using the PCA scores and created a K-means-PCA-model with 4 clusters.

## Purchase Analytics - Positioning
### Data Preprocessing
Applied the segmentation model (scaler.pickle, pca.pickle, kmeans_pca.pickle) to the new dataset (purchase_data.csv) in order to group new customers into clusters.

### Descriptive analysis
* Grouped the data by individual and then by segments to gain insight into customer shopping habits.
* Identified how often each segment group go shopping, how much money they spend and what products they purchase.
* Displayed the standard deviation as a straight line. The bigger the length, the higher the standard deviation is.

### Elasticity Modeling
Price Elasticity, E = % Change in economic outcome of interest (Units sold) / 1% change in price

#### Price Elasticity of Purchase Probability
* Used binomial logistic regression model to determine the probability of purchase where the dependant variable is based on the average price of chocolate candy bars.
* Calculated the price elasticity of purchase probability by segment as well as analyzed the influence of promotion activities.

  E = beta * price * (1-Pr(purchase))
  * |E|<1: inelastic -> increase price
  * |E|>1: elastic -> decrease price

#### Price Elasticity of Brand Choice Probability
* Applied multinomial logistic regression model to predict brand choice probability based on the prices for the five brands.
* Compared own price brand choice elasticity with cross price brand choice elasticity by customer segments.

  E = -beta(own price) * price(cross brand) * Pr(cross brand)
  * E(cross brand) > 0   -> Brands are substitutes for one another
  * |E(cross brand)| > |E(own brand)|   -> The alternative brand is considered a strong substitute


#### Price Elasticity of Purchase Quantity / Price Elasticity of Demand
* Implemented multiple linear regression model to predict the purchase quantity by price and promotion features in the model.
* Calculated the price elasticity of purchase quantity with and without active promotional activities for each price point.

  E = beta * price / quantity(purchase)
