# Customer Purchase Analytics Project Overview

<p float="left">
  <img src="/images/CS_Kmeans_PCA.png"" width=400" />
  <img src="/images/Cross_Brand_Effect.png" width="400" />
</p>

## Part I: Customer Analytics - Segmentation
Customer segmentation to gain insight into the purchase behavior using K-means clustering techniques combined with principal components analysis to reduce the dimensionality of the problem.

## Part II: Purchase Analytics - Positioning
Descriptive and predictive analysis of the purchase behaviour of customers, including price elasticity modeling for purchase probablity, brand choice (own brand and cross brand effects), and purchase quantity.

## Code and Resources
**Python Version:** 3.8

**Packages:** pandas, numpy, sklearn, matplotlib, seaborn, pickle

**Modules:** StandardScaler, KMeans, PCA, LogisticRegression, LinearRegression

**Sources:** [Udemy - Customer Analytics in Python 2020](https://www.udemy.com/course/customer-analytics-in-python/)

## Descriptive Analysis
This part includes:
* Group the data by individual and then by segments to gain insight into customer shopping habits.
* Identify how often each segment group go shopping, how much money they spend and what products they purchase.

## Predictive Analysis - Price Elasticity
Price Elasticity is an important economic and marketing concept that measures how purchasing behavior changes when the price changes. In economics terms, price elasticity stems from the basic economic law of supply and demand.
Following the law of demand, the cheaper the product the higher the demand. The more expensive the product the lower the demand.
It is extremely important for business though because there is a sweet spot which maximizes revenue since revenue is equal to the price times units sold.
This price elasticity concept can be used to find the point at which price times units sold is optimal.

In mathematical terms:

<img src="https://render.githubusercontent.com/render/math?math=Price\: Elasticity,\: E = \frac{Percent\: change\: in\: economic\: outcome\: of\: interest\: (Units\: sold)}{1\: percent\: change\: in\: price}">

There are two cases of price elasticity:
1. **Own Price Elasticity** The elasticity of one product with respect to itself
2. **Cross Price Elasticity:**  The elasticity of one product with respect to the price of another product

### Price Elasticity of Purchase Probability
Price elasticity shows us how much would the purchase probability decreases when the price increases.

<img src="https://render.githubusercontent.com/render/math?math=E = \frac{\Delta Pr(Purchase)}{\Delta Price} * \frac{Price}{Pr(Purchase)} = \beta * \frac{Price}{Pr(Purchase)}">

Price Elasticity | Action
--- | ---
abs(E)<1: inelastic | increase price
abs(E)>1: elastic  | decrease price

This part includes:
* Use binomial logistic regression model to determine the probability of purchase where the dependant variable is based on the average price of the product.
* Calculate the price elasticity of purchase probability by customer segments as well as analyzed the influence of promotion activities.

### Price Elasticity of Brand Choice Probability
Marketer's efforts are devoted to influencing customers to choose namely their brand over competing brands. If the price of a product from a given brand increases the brand choice probability for that brand decreases. Calculating price elasticity of brand choice for a brand with respect to the price of that brand would show us exactly how much.

The choice probability for any one brand and the choice probabilities for all the other brands are interrelated and a marketing mix tool of our brand reflects not only the choice probability for that brand but the choice probabilities for all other brands as well. These effects are known as **own brand effects** and **cross brand effects**.

If another brand increases its unit price, the brand choice probability of the brand of interest would increase. Price elasticity calculations will show us how much the brand choice profitability of our brand would increase with a 1 percent increase in the price of a competing brand.

**Own Brand Effects**

<img src="https://render.githubusercontent.com/render/math?math=E<sub>own brand/sub> = \beta(own\: price) * \frac{Price(own\: price)}{Pr(own\: price)}">

**Cross Brand Effects**

<img src="https://render.githubusercontent.com/render/math?math=E<sub>cross brand</sub> = -\beta(own\: price) * \frac{Price(cross\: brand)}{Pr(cross\: brand)}">

Price Elasticity | Meaning
--- | ---
E<sub>cross brand</sub> > 0 | Brands are substitutes for one another
abs(E<sub>cross brand</sub>) > abs(E<sub>own brand</sub>) | The alternative brand is considered a strong substitute

This part includes:
* Apply multinomial logistic regression model to predict brand choice probability based on the prices for the brands.
* Compared own price brand choice elasticity with cross price brand choice elasticity by customer segments.

### Price Elasticity of Purchase Quantity / Price Elasticity of Demand
Following the law of demand, the greater the unit price of a product the lower the quantity that is going to be purchased. Calculating the price elasticities will show us exactly how the purchase quantities move with the change in price. The percentage change in purchase quantity in response to a one percent change in the unit price of the chosen brand.

<img src="https://render.githubusercontent.com/render/math?math=E = \frac{\Delta Quantity(Purchase)}{\Delta Price} * \frac{Price}{Quantity(Purchase)} = \beta * \frac{Price}{Quantity(Purchase)}">

This part includes:
* Implement multiple linear regression model to predict the purchase quantity by price and promotion features in the model.
* Calculate the price elasticity of purchase quantity with and without active promotional activities for each price point.

<!--

<img align = "left" width = "450" src="/images/CS_Kmeans_PCA.png">
<img align = "right" width = "450" src="/images/Cross_Brand_Effect.png">

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

<p align="center">
  <img src="/images/Pie_Chart_Segment_Proportion.png" width="400" />


<p align="center">
  <img src="/images/PA_Price_Elasticity_of_Purchase_Probability.png" width="600" />

Price Elasticity, E = % Change in economic outcome of interest (Units sold) / 1% change in price
E = beta * price * (1-Pr(purchase))
-->
