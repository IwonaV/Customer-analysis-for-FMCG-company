# Customer-analysis-for-FMCG-company


This analysis is aimed at suggesting the FMCG (fast-moving consumer goods) what to consider when developing marketing and pricing strategies in order to increase revenues from the purchase of a specific brand of chocolate bars. 
For that purpose, STP(Segmentation, Targeting, Positioning) Framework is taken into consideration. For customer’s segmentation were used K-means clustering with PCA (Principal Component Analytics) for dimensionality reduction. Combining clustering results with descriptive statistics allowed for the extraction some interesting insights about revenue distribution by brand and customer segment. 

## Segmentation
### Data Set for Segmentation
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

![image](https://

- We can see a strong positive correlation between the Income vs Occupation and Age vs Education. These are the kind of relationship that will be use in segmentation. As based on the similarities they will be grouped together.

### 2. Standardising the data
We need to treat all the features equally and can achieve that by transforming the feature in such a way that theirs values fall within the same numerical range. Thus the differences between their values would be comparable.

### 3. Hierarchical clustering
The results are returned as a linkage matrix and a Dendrogram is used for plotting the results. 

![image](https://

### 4. K-means clustering
Performing K-means clustering. We consider 1 to 10 clusters, so the for loop runs 10 iterations
Plotting the Within Cluster Sum of Squares for the different number of clusters

![image](https://

### K-mean Clustering Results 

We obtained 4 segments:
-	Segment 1. It is composed of men and women almost equally with the average age of 56. Comparing the mean with the oldest clusters we see that it contains the oldest individuals. More than 2/3 are in relationship and they also have the higher level of education and income. We can call them - Well off Married in their 50s. 
- Segment 2. In this segment 2/3 are male and almost all are single with the average age of 36. Education level is low on average compering to other segments. The salary is also the lowest and they leaving in small cities. We can name it - fewer opportunities. 
- Segment 3. This is the youngest segment with mostly women in a relationship, average age 29. They have a medium level of education, average income and middle management jobs. They seem to be equally distributed between small and mid-size cities. So they seem to be average in every parameter so we can call it - average or standard.
- Segment 4. Mostly men, less than 20% in the relationship, low values in education and high values in income and occupation. Majority of this segment lives in in big or middle-size cities. They are career focused in their 30s.

Plotting the results from the K-means algorithm.

![image](https://

We observed that the cyan segment represents well off cluster is clearly separated. The other three segments are grouped together and it is difficult to distinguish between them. For better result, we will perform PCA to reduce dimensionality and better differentiation of clusters.

### 5. PCA
PCA- Principal Component Analysis is used to find a subset of components, which explain the variance in the data. We have to select the subset of 3 components which preserves about 80% of the variability of the dataset.
The components attribute shows the loadings of each component on each of the seven original features. 
The loadings are the correlations between the components and the original features.

![image](https://

From the results we can see that there is a positive correlation between first component and age, income, occupation and settlement size. These relate to career of a person. This component focused on the career of individual. 
In the second component sex, marital status and education are the most prominent determinants and are rather refer to education and lifestyle.
In the third component age, marital status and occupation are the most important determinants. 



### 6. K-mean in combination with PCA for better clustering solution
After plotting the components, we are able to distinguish the all 4 cluster so the division based on the PCA is much more visible. That is the purpose of PCA to reduces features by combining them into bigger more meaningful ones. Thanks to that we managed to reduce the features from seven into three.

![image](https://





