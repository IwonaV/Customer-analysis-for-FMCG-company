# Customer-analysis-for-FMCG-company


This analysis aims to suggest the FMCG (fast-moving consumer goods) company, what to consider when developing marketing and pricing strategies to increase revenue from the purchase of a specific brand of chocolate bars. 
For that purpose, STP (Segmentation, Targeting, Positioning) framework is taken into consideration.

## 1.Segmentation 

Dividing customers into groups with similar characteristics using of K-means and Principal Component Analytics (PCA) clustering to reduce dimensionality. The combination of clustering results with descriptive statistics allowed for the extraction some interesting insights about revenue distribution by brand and customer segment.  

### Dataset for Segmentation

|                  |     Sex    |     Marital status    |     Age    |     Education    |     Income    |     Occupation    |     Settlement size    |
|------------------|------------|-----------------------|------------|------------------|---------------|-------------------|------------------------|
|     ID           |            |                       |            |                  |               |                   |                        |
|     100000001    |     0      |     0                 |     67     |     2            |     124670    |     1             |     2                  |
|     100000002    |     1      |     1                 |     22     |     1            |     150773    |     1             |     2                  |
|     100000003    |     0      |     0                 |     49     |     1            |     89210     |     0             |     0                  |
|     100000004    |     0      |     0                 |     45     |     1            |     171565    |     1             |     1                  |
|     100000005    |     0      |     0                 |     53     |     1            |     149031    |     1             |     1                  |


The dataset consists of information about the purchasing behaviour of 2,000 individuals from a given area when entering a physical ‘FMCG’ store. All data has been collected through the loyalty cards they use at checkout. The data has been pre-processed and there are no missing values. 

The dataset contains 7 demographic and geographic variables 
Sex, Marital status, age, education, income, occupation, settlement size

- Sex: 0 - male, 1 – female
- Marital status: 0 - single, 1-non-single (divorced / separated / widowed)
- Education: 0 - other / unknown, 1 - high school, 2 - university, 3 - graduate school
- Occupation: 0 – unemployed / unskilled, 1 - skilled employee, 2 - management / self-employed / highly qualified employee
- Settlement size: 0 – small city, 1 - midsized city, 2 – big city


### 1.1. Correlation heat map

Plotting the correlations using a Heat Map.

![image](https://user-images.githubusercontent.com/85560182/162837482-b5a7cce6-e5c4-4dae-84f9-ebf61fcfb459.png)

- There is strong positive correlation between the Income vs Occupation and Age vs Education variables. These are the types of relationship that will be used in segmentation and will be grouped together based on their similarities.

### 1.2. Standardising the data

All the features need to be treated equally and this can be achieved that by transforming them in such a way that theirs values fall within the same numerical range. Thus the differences between their values would be comparable.

### 1.3. Hierarchical clustering

The results are returned as a linkage matrix and a Dendrogram is used for plotting the results. 

![image](https://user-images.githubusercontent.com/85560182/161345264-45042018-7e9b-4807-87ba-85b0dea3b977.png)

### 1.4. K-means clustering

Performing K-means clustering. Considering 1 to 10 clusters, so the for loop runs 10 iterations.
Plotting the Within Cluster Sum of Squares for the different number of clusters

![image](https://user-images.githubusercontent.com/85560182/162837577-ef4ebc0b-9649-44aa-be8f-b71af666d876.png)

### K-mean Clustering Results 

We obtained 4 segments:


|                  |     Sex    |     Marital status    |     Age    |     Education    |     Income    |     Occupation    |     Settlement size    |
|------------------|------------|-----------------------|------------|------------------|---------------|-------------------|------------------------|
|     Segment K-means          |            |                       |            |                  |               |                   |                        |
|     well-off   |    0.501901|	0.692015	|55.703422	|2.129278	|158338.422053|	1.129278	|1.110266	|263	|0.1315               |
|     fewer-opportunities   |  0.352814 |	0.019481 |	35.577922	| 0.746753	| 97859.852814 |	0.329004	| 0.043290	| 462 |	0.2310|
|     standard   |   0.029825	| 0.173684	| 35.635088	| 0.733333	| 141218.249123	| 1.271930	| 1.522807	| 570	| 0.2850|
|     career focused   |   0.853901 |	0.997163	| 28.963121 |	1.068085 |	105759.119149 |	0.634043 |	0.422695	| 705	| 0.3525|

- Segment 1. Composed almost equally of men and women with the average age of 56. Comparing the mean with the oldest clusters we see that it contains the oldest individuals. More than 2/3 are in relationship and they also have the higher level of education and income. We can call them  a wealthy  married couples in their 50s. – Well off
- Segment 2. In this segment 2/3 are men and almost all are single people with an average age of 36. The level of education is on average low compared to other segments. The salary is also the lowest and they live in small cities. We can name it - Fewer opportunities. 
- Segment 3. This is the youngest segment where predominate women in relationship, average age 29. They have a medium level of education, average income and middle management jobs. They seem to be equally distributed between small and mid-size cities. So they seem to be average in every parameter so we can call it - Average or Standard.
- Segment 4. Mostly men, less than 20% in the relationship, low values in education and high in income and occupation. Most of this segment lives in in large or middle-size cities. They are career focused in their 30s.

Plotting the results from the K-means algorithm.

![image](https://user-images.githubusercontent.com/85560182/161345370-c1c46ed3-9451-4373-b2de-bdef349e3238.png)

We observed that the cyan segment represents Well off cluster is clearly separated. The other three segments are grouped together and it is difficult to distinguish between them. For better result, we will perform PCA to reduce dimensionality and better differentiation of clusters.

### 1.5. PCA

Principal Component Analysis is used to find a subset of the components that explain the variance of the data. We need to select the subset of 3 components which preserves about 80% of the variability of the dataset.
The components attribute shows the loadings of each component of each of the seven original features. 
The loadings are the correlations between the components and the original features.
In this visual We can see explained variance by components.

![image](https://user-images.githubusercontent.com/85560182/161862577-f20d38de-71aa-4724-9877-f9882aaf3358.png)

Plotting the loadings using a Heat Map.

![image](https://user-images.githubusercontent.com/85560182/162837656-4f56ecc2-7cd5-4046-8f34-c083383925c2.png)

The results show that there is a positive correlation between the first component and age, income, occupation and settlement size. These relate to career of a person. This component focused on the career of individual. 
In the second component, sex, marital status and education are the most prominent determinants and relate rather to education and lifestyle.
In the third component, age, marital status and occupation are the most important determinants. 


### 1.6. K-mean in combination with PCA for better clustering solution

After plotting the components, we are able to distinguish the all 4 cluster so the division based on the PCA is much more visible. It is the goal of PCA to reduces features by combining them into large more meaningful ones. Thanks to this we were to reduce the features from seven to three.

![image](https://user-images.githubusercontent.com/85560182/162837761-79149fc9-c69f-4216-83ef-830d1c2d2717.png)
![image](https://user-images.githubusercontent.com/85560182/162837789-f721b679-f87a-4066-bbbe-848efd88e0ff.png)
![image](https://user-images.githubusercontent.com/85560182/162837820-f706af6b-2d8c-4d1c-b037-91873548bf7d.png)

## 2. Purchase Descriptive Analytics 

Marketing mix is the main approach to positioning and this analysis will focus on customer behaviour in terms of purchase probability, brand choice probability, and purchase quantity.  
For this purpose, the machine learning algorithms (linear regression and logistic regression) were implemented.

### Dataset for Segmentation

The dataset consists of information about the purchases of chocolate bars of 500 individuals from a given area when entering a physical ‘FMCG’ store over a 2-year period. All data has been collected through the loyalty cards they use at checkout. The data has been pre-processed and there are no missing values.


|          |     ID           |     Day    |     Incidence    |     Brand    |     Quantity    |     Last_Inc_Brand    |     Last_Inc_Quantity    |     Price_1    |     Price_2    |     Price_3    |     ...    |     Promotion_4    |     Promotion_5    |     Sex    |     Marital status    |     Age    |     Education    |     Income    |     Occupation    |     Settlement size    |     Segment    |
|----------|------------------|------------|------------------|--------------|-----------------|-----------------------|--------------------------|----------------|----------------|----------------|------------|--------------------|--------------------|------------|-----------------------|------------|------------------|---------------|-------------------|------------------------|----------------|
|     0    |     200000001    |     1      |     0            |     0        |     0           |     0                 |     0                    |     1.59       |     1.87       |     2.01       |     ...    |     0              |     0              |     0      |     0                 |     47     |     1            |     110866    |     1             |     0                  |     0          |
|     1    |     200000001    |     11     |     0            |     0        |     0           |     0                 |     0                    |     1.51       |     1.89       |     1.99       |     ...    |     0              |     0              |     0      |     0                 |     47     |     1            |     110866    |     1             |     0                  |     0          |
|     2    |     200000001    |     12     |     0            |     0        |     0           |     0                 |     0                    |     1.51       |     1.89       |     1.99       |     ...    |     0              |     0              |     0      |     0                 |     47     |     1            |     110866    |     1             |     0                  |     0          |
|     3    |     200000001    |     16     |     0            |     0        |     0           |     0                 |     0                    |     1.52       |     1.89       |     1.98       |     ...    |     0              |     0              |     0      |     0                 |     47     |     1            |     110866    |     1             |     0                  |     0          |
|     4    |     200000001    |     18     |     0            |     0        |     0           |     0                 |     0                    |     1.52       |     1.89       |     1.99       |     ...    |     0              |     0              |     0      |     0                 |     47     |     1            |     110866    |     1             |     0                  |     0          |

The data explanation:
- Incidence: 0 -The customer has not purchased an item from the category of interest, 1 - The customer has purchased an item from the category of interest
- Brand: 0 - No brand was purchased, 1 -  Brand ID the customer has purchased
- Last_Inc_Brand: 0 - No brand was purchased, {1,2,3,4,5} - brand ID the customer has purchased on their previous store visit
- Price_1:  Price of an item from Brand 1 on a particular day
- Price_2:  Price of an item from Brand 2 on a particular day
- Price_3:  Price of an item from Brand 3 on a particular day
- Price_4:  Price of an item from Brand 4 on a particular day
- Price_5:  Price of an item from Brand 5 on a particular day
- Promotion_1:  0 - Brand 1 was not on promotion or not on a particular day, 1 - Brand 1 was on promotion or not on a particular day
- Promotion_2:  0 - Brand 2 was not on promotion or not on a particular day, 1 - Brand 2 was on promotion or not on a particular day
- Promotion_3:  0 - Brand 3 was not on promotion or not on a particular day, 1 - Brand 3 was on promotion or not on a particular day
- Promotion_4:  0 - Brand 4 was not on promotion or not on a particular day, 1 - Brand 4 was on promotion or not on a particular day
- Promotion_5:  0 - Brand 5 was not on promotion or not on a particular day, 1 - Brand 5 was on promotion or not on a particular day
- Sex: 0 - male, 1 – female
- Marital status: 0 - single, 1-non-single (divorced / separated / widowed)
- Education: 0 - other / unknown, 1 - high school, 2 - university, 3 - graduate school
- Occupation: 0 – unemployed / unskilled, 1 - skilled employee, 2 - management / self-employed / highly qualified employee
- Settlement size: 0 – small city, 1 - midsized city, 2 – big city

### Applying the segmentation model 

An important part of the analytics is knowing how the customers are similar to each other. Therefore, the insights gained so far will be used and the new customers will be placed within four clusters that were determined. The data needs to be pre-processed the same way as when building the customer segmentation model.
To standardise the variables, it is necessary to import the scaler and PCA object and the data will be transformed by using them. 

### 2.1. Descriptive Analysis by Segments

Building purchase behaviour model and analysing purchase behaviour of the segments. 
Starting from calculating number of visits, number of purchases and average number of purchases and which segment customers belong to, then calculating the segment proportions. Calculating the mean of average purchases by the four segments would help to determine the average customer behaviour in each segment.
Gained information can be used to calculate the segment proportions, by grouping each segment.

### Proportions of the purchases by segment 

![image](https://user-images.githubusercontent.com/85560182/162837988-4888d44e-6044-44f4-83bc-8b5d0220e25f.png)

It is clearly visible that the largest segment is fewer- opportunities followed by career focused individuals. 

### 2.2 Purchase occasion and purchase incidence 

Calculating the mean of average purchases by the four segments would help to determine the average customer behaviour in each segment.

### The average number of store visits

Using the bar chart to visualize how often the people from different segment visit the store. 

![image](https://user-images.githubusercontent.com/85560182/162838129-e1764b73-46f7-47a9-b6de-760df4834bc3.png)

Looking at the bar chart it is visible which segment visit the sore the most. Career focused is the most frequent but at the same time the standard deviation is quite high, this imply that the individuals within this segment are least homogenous, that is least alike when it comes to how often they visit the grocery store.

### Number of purchases by segment

![image](https://user-images.githubusercontent.com/85560182/162838158-e624981a-0cec-4ad1-a1a9-2f21cf6a9c23.png)

It can be observed that the career focused segments buys the product more often but at the same time its standard deviation is the highest. The most homogenous segment is the fewer opportunities also standard segment is consistent.
 

### 2.3. Brand Choice

Which brand is the customer going to choose?
Taking into account the occasions when the chocolate bar was purchased. 
The heat map shows average brand choice by segment. Where Brand 1 is the cheapest and Brand 5 is the most expensive.	
![image](https://user-images.githubusercontent.com/85560182/162838267-782cc679-399b-4bda-ab26-f145c14ccabe.png)

From the result is visible that almost 70% of Fewer opportunities segment strongly prefer the Brand 2 which is not the cheapest one, where 62% of Career focused segment prefer the most expensive one -Brand 5, which can indicate that this segment is looking for some kind of luxury status. Interestingly the Well-off segment prefers the more luxurious brand but not the most expensive -Brand 4.
Looking at the Standard segment we can see that is the most heterogeneous one as the preferences are scatter across all brands. 
- If looking for actionable insight one idea could be influencing them to try out different brands. This insight is very interesting but it doesn’t really explain how they affect the bottom line so exploring revenue by segment is the next step. 

### 4. Revenue By Segment 

Calculating revenue for each brand by segment and total revenue for each of the four segments.
Modifying the table to take into account the proportion of the segments will allow us to see the size of the segment compared to the revenue they bring.


|                            |     Revenue Brand 1    |     Revenue Brand 2    |     Revenue Brand 3    |     Revenue Brand 4    |     Revenue Brand 5    |     Total Revenue    |     Segment Proportions    |
|----------------------------|------------------------|------------------------|------------------------|------------------------|------------------------|----------------------|----------------------------|
|     Segment                |                        |                        |                        |                        |                        |                      |                            |
|     Fewer-Opportunities               |     2258.90            |     13909.78           |     722.06             |     1805.59            |     2214.82            |     20911.15         |     0.378                  |
|     Career-Focused         |     736.09             |     1791.78            |     664.75             |     2363.84            |     19456.74           |     25013.20         |     0.222                  |
|     Standard    |     2611.19            |     4768.52            |     3909.17            |     861.38             |     2439.75            |     14590.01         |     0.206                  |
|     Well-Off               |     699.47             |     1298.23            |     725.54             |     14009.29           |     5509.69            |     22242.22         |     0.194                  |



Analysing the result, we can see that the Career focused segment bring the most revenue follow by the Well- off and Fewer opportunities segments. The Standard segment is smallest in contribution to the revenue. Looking at the segment proportion the Career-focused is also the largest. The Well- off and Fewer- opportunities segments spend around the same amount of money on the chocolate bars. However, the Fewer- opportunities segment double the size of Well – off segment.
Looking from the perspective of the individual brands we can see that the Brand 3 has the lowest revenue and its higher contributor is the Standard segment. 
So if we looking at the actionable ideas, reducing the price of Brand 3 could encourage that segment to buying this product even more. 
Brand 4 is popular in Well-off segment which also is a big buyer of Brand 5. So it seems that loyalty is the biggest factor. Here we can take into account the slight increase in the price of these brands.

## 3. Purchase Predictive Analytics

 ### 3.1. Purchase Incidence 
 
In this part of analysis, a statistical model is used that estimates purchase probability for each customer at each shopping trip. Also the price elasticity of purchase probability under different condition will be calculated.  
Before starting to build the model the data needs to be pre-process the same way as in descriptive part of analysis. 

###  Model building

The model: binomial logistic regression – is a classification method which outputs a probability between 0 and 1.
Choosing dependent and independent variable in the model. 
‘Incidence’- dependent variable (predicting probability of purchase)
Y = df_pa['Incidence']
Purchase probably is influences by price so that will be the predictor (independent variable)
X = price (independent)
X = pd.DataFrame()
X['Mean_Price'] = (df_pa['Price_1'] +
                   df_pa['Price_2'] +
                   df_pa['Price_3'] +
                   df_pa['Price_4'] +
                   df_pa['Price_5'] ) / 5

The chosen model is logistic regression. Fitting the model with X and Y we get the results for the mean price. 
The coefficient is -2.345 which means that increase in price decrees purchase probability. 

### Price Elasticity of Purchase Probability

Calculating the price elasticity and the price elasticity with the promotion then compering elasticity and how much the probability of purchasing will change. 
By using describe method we can see that the price ranges from min 1.1 to max 2.8. Therefore, we'll choose a range between 0.5 and 3.5 to get a better understanding how the purchase probabilities and respective elasticity has changed.


|       | Price_1  | Price_2  | Price_3  | Price_4  | Price_5  |
|-------|----------|----------|----------|----------|----------|
| count |    58693 |    58693 |    58693 |    58693 |    58693 |
|  mean | 1.392074 | 1.780999 | 2.006789 | 2.159945 | 2.654798 |
|   std | 0.091139 | 0.170868 | 0.046867 | 0.089825 | 0.098272 |
|   min |      1.1 |     1.26 |     1.87 |     1.76 |     2.11 |
|   25% |     1.34 |     1.58 |     1.97 |     2.12 |     2.63 |
|   50% |     1.39 |     1.88 |     2.01 |     2.17 |     2.67 |
|   75% |     1.47 |     1.89 |     2.06 |     2.24 |      2.7 |
|   max |     1.59 |      1.9 |     2.14 |     2.26 |      2.8 |


Predicting the purchase probability for our newly defined price range, we can easily see that for lower price the purchase probability is higher and vice versa. By calculating the price elasticity, we can predict how the demand for a product changes for the given price change.
Elasticity = beta*price*(1-P(purchase))
pe = model_purchase.coef_[:, 0] * price_range * (1 - purchase_pr)
Representing data frame as a graph to see the elasticity curve and how it changes comparing to the price range. 

 ## ----------Image 

As a function, price elasticity decreases as the price increases. The decrease of the price is slow in the range 0.5 and 1.1 and then became steeper.
Thus, an increase in elasticity of 1% leads to decrease of less than 1% of purchase probability. Therefore, purchase probability at this point is inelastic. 
For inelastic values general recommendation is to increase the price as it would not cause significant decrease in the purchase probability. On the other hand, if we have the elasticity which is greater than 1, we should lower the prices.
In this case if the price is lower than 1.25, we can increase the product price as the purchase probability would not change much. However, for prices higher than 1.25, we would gain more by reducing the prices.
The obtained results are valuable, but we need to refine this analysis examining each segment individually.

### Purchase Probability by Segments

## --------image

Tipping points for all the segments:
average – 1.25
Segment 0 (fewer opportunities)- 1.27
Segment 1(career – focused) -  1.38
Segment 2 (standard) – 1.23
Segment 3 (well off) - 1.45

Fewer Opportunities segment is more price sensitive (the most elastic) compared to the other segments. The line is not only lower that the other but also much steeper, which means that as the price increases, it become more elastic much faster. Its tipping point is 1.27 which is higher than the Standard segment which means it tends to be more inelastic at lower prices.
These customers seem to like the candy bars so much that they are unaffected by rising prices in the low price range, but when the price became too expensive they don’t want to buy it any more.  

### Purchase Probability with Promotion Feature

In the purchase analysis model, price is the most characteristic and product promotion can affect purchase probability therefore in this model we incorporate the product promotion feature to see its effect on elasticity. 
The model quantifies the exact relationship between price, promotion and probability of purchase.

Modelling purchase probability where:
Y = df_pa['Incidence']
X will include the price feature 
X = pd.DataFrame()
X['Mean_Price'] = (df_pa['Price_1'] + 
                   df_pa['Price_2'] + 
                   df_pa['Price_3'] + 
                   df_pa['Price_4'] + 
                   df_pa['Price_5']) / 5
                   
Including a second promotion feature to examine the effects of promotions on purchase probability.
Calculating the average promotion rate across the five brands. 
X['Mean_Promotion'] = (df_pa['Promotion_1'] +
                       df_pa['Promotion_2'] +
                       df_pa['Promotion_3'] +
                       df_pa['Promotion_4'] +
                       df_pa['Promotion_5'] ) / 5

Estimate the logistic regression model and fitting it with Y and new X data frame. 
Obtained coefficients:
For the price: -1.49392709, it is negative. 
For promotion: 0.56148565, it is positive that means with the increase in promotion the purchase probability will also increase.

### Price Elasticity with Promotion 

We are interested in the overall impact of promotional activities on elasticities and here are two cases:
1.	Promotional activities for all brands. 
2.	No promotional activities.
The graph represents the results

## ----image 

These two lines represent the purchase probabilities given maximum and minimum promotional activities. We can see that the line represents the elasticity with promotion is located above the non-promotion elasticity for the entire price range. 
Additionally, check the master data frame for the tipping point we can see that inelasticity with promotion ends at 1.27 while elasticity with promotion at 1.46 making customers less sensitive to price changes during promotional activities. This means that it would be more beneficial to have a higher original price and permanent promotion rather than lower original price.

### 3.2.  Brand Choice Probability

The final goal of the model is to determine what the probability of choosing a given brand is.
Focusing on the ‘brand’ variable and which one was purchased. In such a situation calculating brand choice probability is necessary to analyse customer’s behaviour that can increase sales and at the same time increase customer satisfaction.
Since there are 5 different classes (brands of chocolates) multinomial logistic regression is used.

Building the regression model to determine the customer choice of the brand.
Y = brand choice['Brand']  

Prediction will be based on the prices for the five brands. 
features = ['Price_1', 'Price_2', 'Price_3', 'Price_4', 'Price_5']
X = brand choice [features] 

Fitting the model with the input X and target Y

We estimate the beta values (coefficients) that show how the choice probability for own brand and choice probability for other brands are interrelated. In general, brand choice probability increases if its own price is lower and other brands' prices are higher and vice versa.

|                |     Coef_Brand_1    |     Coef_Brand_2    |     Coef_Brand_3    |     Coef_Brand_4    |     Coef_Brand_5    |
|----------------|---------------------|---------------------|---------------------|---------------------|---------------------|
|     Price_1    |     -3.92           |     1.27            |     1.62            |     0.57            |     0.44            |
|     Price_2    |     0.66            |     -1.88           |     0.56            |     0.40            |     0.26            |
|     Price_3    |     2.42            |     -0.21           |     0.50            |     -1.40           |     -1.31           |
|     Price_4    |     0.70            |     -0.21           |     1.04            |     -1.25           |     -0.29           |
|     Price_5    |     -0.20           |     0.59            |     0.45            |     0.25            |     -1.09           |  

The coefficient for Brand 1 is negative for its own price but positive for all other except for Brand 5. The higher the price for their own brand products the probability for buying the competitors brand increase.

### Own Price Elasticity for Brand 5

Performing brand choice analysis is useful from a brand perspective. Therefore, we will focus on Brand 5 to gain insight in developing marketing strategy to target customers. 

## ---------	Image 

Based on the visualization we can see how the Brand 5 purchase probability changes when its own price changes.

### Cross Price Elasticity Brand 5, Cross Brand 4

It is interesting to see what happens to purchase probability of brand 5 if a competitor changes their pricing.

We can examine the relationship between own Brand 5 and the competing Brand 4 and determine the cross price elasticity of Brand 5 with respect to Brand 4.
Cross price elasticity measures the purchase probability for our own brand based on competitor’s price change, hence we need to examine the changes in Brand 4.

Computing the product probability using our model brand choice using the formula:

### E = -beta (own price) * price (cross brand) *Pr (cross brand)

The results:

## ---Image

It is visible that the elasticities are positive throughout the price range. This indicates that if the competitor’s Brand 4 increases prices the purchase probability for own brand 5 would increase. When a competitor rises their price, customers start buying own brand product more and the elasticity show us exactly how much more. 

Depending on cross price elasticities we can gain the insights about the market itself. If the cross price elasticity is greater than zero, the two products are considered substitutes.

### E (cross brand) > 0       substitute

In this analysis all cross price elasticities are positive as all brands are substitutes for one another furthermore if the cross price elasticity at some point is grater in an absolute term then our own price elasticity is considered a strong substitute.

### |E (cross brand) | >|E (own brand) |      strong substitute 

- Brand 4 is a strong substitute for Brand 5 for all prices up to $1.65.
- If Brand 4 has substantially lower price it would be a very strong competitor at Brand 5.
- The observed price range of Brand 4 is between $1.76 and $2.6, in this region the elasticity steadily decreasing which signals as the price increases the purchase probability changes slower but is still positive, which means that our purchase probability still increases with the increase in price of Brand 4 but at a slower rate.
- These prices are outside natural domain of Brand 4, therefore if Brand 4 had a substantially lower its price it would be a very strong competitor for Brand 5
- Even though the elasticity is starting to decrease from the 1.45 mark, it is still positive, signalling that the increase in purchase probability for Brand 5 is slower.
- When it comes to average customer, Brand 4 is a weak substitute for Brand 5 
- Brand 5 can create a marketing strategy targeting customers who choose Brand 4, and attract them to buy own Brand 5.

### Own and Cross-Price Elasticity by Segment

We are interested in analysing the purchase probability for choosing brand 5 by each of the segment. 

## -----image 

Plotting the own and cross brand price elasticities for the average customer and each of the four segments allows us observe differences and similarities between the segments and examine their preference, when it comes to brand choice.

The two segments, which seem to be most interesting for targeting with brand 5, are Career-focused and the Well-off. They are also the segments which purchase this brand most often. 
-	The Career-focused segment is the most inelastic and its customers are tending to be loyal and are not influence much by price.  Therefore, brand 5 could increase its price, without fear of significant loss of customers. The cross price elasticity shows low values, which indicates that these customers are unlikely to switch to brand 4.
-	The Well-off segment seems to be more elastic. These customers also purchase the competitor brand 4 most often. Therefore, in order to target this segment price needs to be decreased. 

## 3.3 Purchase Quantity

To determine price elasticity of purchase quantity, also known as price elasticity of demand, we're interested in purchase occasion, where the purchased quantity is different from 0. 

### Model building

Model - Linear regression 
Choosing dependent and independent variable in the model. 
Independent variable: price, promotion 
X = df_purchase_quantity[['Price_Incidence', 'Promotion_Incidence']]
Dependent variable: quantity
Y = df_purchase_quantity['Quantity']

The coefficients for price and promotion are both negative. 
array([-0.8173651 , -0.10504673])

It appears that promotion have a negative impact on the purchase quantity of the average client which is unexpected.

### Price Elasticity of Purchase Quantity with and without Promotional Activities

We examine the price elasticity of purchase quantity with and without promotional activities for each price point.

Calculate the price elasticity the formulas:
price_elasticity_quantity_promotion_yes = beta_quantity * price_range / predict_quantity
price_elasticity_quantity_promotion_no = beta_quantity * price_range / predict_quantity

## ----image

Plotting the two elasticities side by side we observe that the two elasticities are very close together for almost the entire price range.
The insights we gained are implying that that promotion does not appear to be a significant factor in customer decision about how many chocolate candy bars to purchase.



