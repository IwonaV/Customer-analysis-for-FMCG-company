# Customer-analysis-for-FMCG-company


This analysis aims to suggest the FMCG (fast-moving consumer goods) company, what to considered when developing marketing and pricing strategies in order to increase revenue from the purchase of a specific brand of chocolate bars. 
For that purpose, STP(Segmentation, Targeting, Positioning) framework is taken into consideration.

The analysis consists of two parts:
1. Segmentation 
Performing K-means clustering with PCA (Principal Component Analytics) for dimensionality reduction. Combining clustering results with descriptive statistics allowed for the extraction some interesting insights about revenue distribution by brand and customer segment. 
2. Positioning 
The marketing mix is the main approach to positioning and this analysis will focus on customer behaviour in terms of purchase probability, brand choice probability, and purchase quantity.  
For that purpose the machine learning algorithms linear regression and logistic regression were implemented.


## Segmentation
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

The data has been mapped with the values:
- Sex: 0 - male, 1 – female
- Marital status: 0 - single, 1-non-single (divorced / separated / widowed)
- Education: 0 - other / unknown, 1 - high school, 2 - university, 3 - graduate school
- Occupation: 0 – unemployed / unskilled, 1 - skilled employee, 2 - management / self-employed / highly qualified employee
- Settlement size: 0 – small city, 1 - midsized city, 2 – big city

### 1. Correlation heat map
Plotting the correlations using a Heat Map.

![image](https://user-images.githubusercontent.com/85560182/161345059-5ac6e78b-80ab-4c6c-a5a8-1124e591d512.png)


- We can see a strong positive correlation between the Income vs Occupation and Age vs Education. These are the kind of relationship that will be used in segmentation. As based on the similarities they will be grouped together.

### 2. Standardising the data
We need to treat all the features equally and can achieve that by transforming the feature in such a way that theirs values fall within the same numerical range. Thus the differences between their values would be comparable.

### 3. Hierarchical clustering
The results are returned as a linkage matrix and a Dendrogram is used for plotting the results. 

![image](https://user-images.githubusercontent.com/85560182/161345264-45042018-7e9b-4807-87ba-85b0dea3b977.png)

### 4. K-means clustering
Performing K-means clustering. We consider 1 to 10 clusters, so the for loop runs 10 iterations
Plotting the Within Cluster Sum of Squares for the different number of clusters

![image](https://user-images.githubusercontent.com/85560182/161345308-f16774dd-8dbe-491c-b3a4-7ff3967d8f27.png)

### K-mean Clustering Results 

We obtained 4 segments:


|                  |     Sex    |     Marital status    |     Age    |     Education    |     Income    |     Occupation    |     Settlement size    |
|------------------|------------|-----------------------|------------|------------------|---------------|-------------------|------------------------|
|     Segment K-means          |            |                       |            |                  |               |                   |                        |
|     well-off   |    0.501901|	0.692015	|55.703422	|2.129278	|158338.422053|	1.129278	|1.110266	|263	|0.1315               |
|     fewer-opportunities   |  0.352814 |	0.019481 |	35.577922	| 0.746753	| 97859.852814 |	0.329004	| 0.043290	| 462 |	0.2310|
|     standard   |   0.029825	| 0.173684	| 35.635088	| 0.733333	| 141218.249123	| 1.271930	| 1.522807	| 570	| 0.2850|
|     career focused   |   0.853901 |	0.997163	| 28.963121 |	1.068085 |	105759.119149 |	0.634043 |	0.422695	| 705	| 0.3525|

-	Segment 1. It is composed of men and women almost equally with the average age of 56. Comparing the mean with the oldest clusters we see that it contains the oldest individuals. More than 2/3 are in relationship and they also have the higher level of education and income. We can call them - Well off Married in their 50s. 
- Segment 2. In this segment 2/3 are male and almost all are single with the average age of 36. Education level is low on average compering to other segments. The salary is also the lowest and they leaving in small cities. We can name it - fewer opportunities. 
- Segment 3. This is the youngest segment with mostly women in a relationship, average age 29. They have a medium level of education, average income and middle management jobs. They seem to be equally distributed between small and mid-size cities. So they seem to be average in every parameter so we can call it - average or standard.
- Segment 4. Mostly men, less than 20% in the relationship, low values in education and high values in income and occupation. Majority of this segment lives in in big or middle-size cities. They are career focused in their 30s.

Plotting the results from the K-means algorithm.

![image](https://user-images.githubusercontent.com/85560182/161345370-c1c46ed3-9451-4373-b2de-bdef349e3238.png)

We observed that the cyan segment represents well off cluster is clearly separated. The other three segments are grouped together and it is difficult to distinguish between them. For better result, we will perform PCA to reduce dimensionality and better differentiation of clusters.

### 5. PCA
PCA- Principal Component Analysis is used to find a subset of components, which explain the variance in the data. We have to select the subset of 3 components which preserves about 80% of the variability of the dataset.
The components attribute shows the loadings of each component on each of the seven original features. 
The loadings are the correlations between the components and the original features.
From this visual We can see explained variance by components.

![image](https://user-images.githubusercontent.com/85560182/161862577-f20d38de-71aa-4724-9877-f9882aaf3358.png)

Plotting the loadings using a Heat Map

![image](https://user-images.githubusercontent.com/85560182/161345420-83e55e3e-5ca7-4c66-acf5-1c8391d5e65e.png)

From the results we can see that there is a positive correlation between first component and age, income, occupation and settlement size. These relate to career of a person. This component focused on the career of individual. 
In the second component sex, marital status and education are the most prominent determinants and are rather refer to education and lifestyle.
In the third component age, marital status and occupation are the most important determinants. 


### 6. K-mean in combination with PCA for better clustering solution
After plotting the components, we are able to distinguish the all 4 cluster so the division based on the PCA is much more visible. That is the purpose of PCA to reduces features by combining them into bigger more meaningful ones. Thanks to that we managed to reduce the features from seven into three.

![image](https://user-images.githubusercontent.com/85560182/161345487-352803d8-553a-497d-8071-499da555eac5.png)
![image](https://user-images.githubusercontent.com/85560182/161345507-3ec95014-0cd1-4c8b-8060-67dbfcd22760.png)
![image](https://user-images.githubusercontent.com/85560182/161345524-00eb6bff-d89a-4128-9555-c719b14006a1.png)

## Positioning
Here we try to answer the questions:
2.	Will the customer buy the product from a particular product category when they enter the shop? 
3.	Which brand is the customer going to choose 
4.	How many units is the customer going to purchase?
5.	


### Segmentation data

The dataset consists of information about the purchases of chocolate  bars of 500 individuals from a given area when entering a physical ‘FMCG’ store in the period of 2 years. All data has been collected through the loyalty cards they use at checkout. The data has been preprocessed and there are no missing values.


|          |     ID           |     Day    |     Incidence    |     Brand    |     Quantity    |     Last_Inc_Brand    |     Last_Inc_Quantity    |     Price_1    |     Price_2    |     Price_3    |     ...    |     Promotion_4    |     Promotion_5    |     Sex    |     Marital status    |     Age    |     Education    |     Income    |     Occupation    |     Settlement size    |     Segment    |
|----------|------------------|------------|------------------|--------------|-----------------|-----------------------|--------------------------|----------------|----------------|----------------|------------|--------------------|--------------------|------------|-----------------------|------------|------------------|---------------|-------------------|------------------------|----------------|
|     0    |     200000001    |     1      |     0            |     0        |     0           |     0                 |     0                    |     1.59       |     1.87       |     2.01       |     ...    |     0              |     0              |     0      |     0                 |     47     |     1            |     110866    |     1             |     0                  |     0          |
|     1    |     200000001    |     11     |     0            |     0        |     0           |     0                 |     0                    |     1.51       |     1.89       |     1.99       |     ...    |     0              |     0              |     0      |     0                 |     47     |     1            |     110866    |     1             |     0                  |     0          |
|     2    |     200000001    |     12     |     0            |     0        |     0           |     0                 |     0                    |     1.51       |     1.89       |     1.99       |     ...    |     0              |     0              |     0      |     0                 |     47     |     1            |     110866    |     1             |     0                  |     0          |
|     3    |     200000001    |     16     |     0            |     0        |     0           |     0                 |     0                    |     1.52       |     1.89       |     1.98       |     ...    |     0              |     0              |     0      |     0                 |     47     |     1            |     110866    |     1             |     0                  |     0          |
|     4    |     200000001    |     18     |     0            |     0        |     0           |     0                 |     0                    |     1.52       |     1.89       |     1.99       |     ...    |     0              |     0              |     0      |     0                 |     47     |     1            |     110866    |     1             |     0                  |     0          |

The data has been mapped with the values:
- Incidence: 0 -The customer has not purchased an item from the category of interest, 1 - The customer has purchased an item from the category of interest
- Brand: 0 - No brand was purchased, 1 -  Brand ID the customer has purchased
- Last_Inc_Brand: 0 - No brand was purchased, {1,2,3,4,5} - brand ID the customer has purchased on their previous store visit
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
- 

### Applying the segmentation model 

An important part of the analytics is knowing how the customers are similar to each other’s. So we’ll use the insights we’ve gain so far and we place the new customers to 4 clusters we have determined. So the data needs to be pre-processed the same way how when building the customer segmentation model.
To standardise the variables, we will import the scaler and PCA object but will not fit them instead we will transform the data by using them.

### 1. 𝐃𝐞𝐬𝐜𝐫𝐢𝐩𝐭𝐢𝐯𝐞 𝐀𝐧𝐚𝐥𝐲𝐬𝐢𝐬 𝐛𝐲 𝐒𝐞𝐠𝐦𝐞𝐧𝐭𝐬

So I will be building purchase behaviour model and analysing purchase behaviour of the segments. 
Starting from calculating number of visits, number of purchases and average number of purchases and which segment they belong and calculating the segment proportions. 
Next calculating the mean of average purchases by the four segments would help to determine the average customer behaviour in each segment.

- table with number of visitts, nr purchases etc. 

the information we gain we can use it to calculate the segment proportions, by gruping by the each segment.

# Segment Proportions

### 1. Proportions of the purchases by segment 

image - segment proportion

It is clearly visible that the largest segment is fewer- oportunities followed by career focused individuals. 

### 2.  𝐏𝐮𝐫𝐜𝐡𝐚𝐬𝐞 𝐎𝐜𝐜𝐚𝐬𝐢𝐨𝐧 and a𝐮𝐫𝐜𝐡𝐚𝐬𝐞 𝐈𝐧𝐜𝐢𝐝𝐞𝐧𝐜𝐞

Next calculating the mean of average purchases by the four segments would help to determine the average customer behaviour in each segment.

### The average number of store visits

Using the bar chart to visualize how ofter the people from diferent segment visit the store. 

- image 

So looking at the bar chart we can see which segment visit the sore the most and we can see that career focused is the most frequent but at the same time the standard deviation quite high, this imply that the individuals within this segment are least homogenous, that is least alike when it comes to how often they visit the grocery store.

### Number of purchases by segment

image 

we observed that the career focused segments buys the product more often but at the same time its standard deviation is the highest. the most homogenues segment is the fewer oporunities. also standatd segment is consistent with  

### 3. Brand choice

which brand is the customer going to choose?
for this porpose made dummies for each of the five brands
-	So I have to concentrate only on the occasions when the chocolate bar was purchased and for better understanding I created the heat map of average brand choice by segment. where Brand 1 is the chipperst and Brabd 5 most expensive.

-  image heat map of brand choice 

And from the result is visible that almost 70% of fewer oportunities segment strongly prefer the brand 2  which is not the chippest one, where else 63% of career focused segment prefer the most expensive one -Brand 5 which can indicate that this segment is looking for some kind of luxury status. and this can be the oportunity to rise the price of brand 5 even further. interestingly the well off segment prefers the more luxurius brand but not the most expensive -Brand 4.
looking at the standard segment we can see that is the most heterogenious one as the preferences are scater all arount the brands. 
- if looking for actionable insight one idea is to tring influence them to try out diferent brands. This insight are very interesing but they dont really explain how they afect the botom line so exporing reveniu by segment is the next step.

### 4. Revenue by segment 













