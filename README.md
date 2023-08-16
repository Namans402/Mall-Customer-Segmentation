# Mall Customer Segmentation
___
 
## Project Goal

A mall has approached us with customer information and tasked us with increasing the malls profits. Our goal here is to use clustering to find potential groups of customers 
and extract characteristics from the groups.

## Dataset

The dataset I found was acquired using Kaggle but is also in this folder. It has customer sex, age, annual income, and spending score.

## Process

#### Data Preprocessing:
   - Missing Data:
      - using dataframe.info() we see that there are 200 entries overall and all columns have 200 rows, so there is no missing data
   - Data Exploration:
      - use pairplot and found 2 relationships, spending score and age: young people buy more, spending score and annual income: relationship unknown
      - ![Capture](https://user-images.githubusercontent.com/32663193/122116722-f10f7080-cdf3-11eb-98d0-72c79cebcdb2.PNG)
   - Data Encoding:
      - encode gender however this isn't necessary as gender doesn't seem to play a role in this relationship
   - Feature Selections:
      - select spending score and annual income

#### Model:
We should use K-Means and Gaussian-Mixtures (GMM) as they are popular clustering models<br>
   - K-Means
      - use silhouette analysis to find ideal number of clusters
      - plot clusters with cluster radius and cluster center 
   - GMM
      - use AIC and BIC to find ideal number of clusters (you can use elbow method too if you like)
      -  plot clusters with cluster radius

## Results

For K-Means the silhouette analysis for clusters 5, 6 and 7 will be displayed below, these clusters had the highest score however as you will see. 
5 clusters was originally how I would cluster the data. 
6 clusters looked a bit weird as it seemed to pick up some outliers but not all.
7 clusters look like 5 clusters but also captures the outliers better than 6 clusters.

![Capture1](https://user-images.githubusercontent.com/32663193/122119020-bbb85200-cdf6-11eb-92a6-f5ae2df27a73.PNG)
![Capture2](https://user-images.githubusercontent.com/32663193/122119036-c07d0600-cdf6-11eb-8685-c98ded5f2b19.PNG)
![Capture3](https://user-images.githubusercontent.com/32663193/122119046-c2df6000-cdf6-11eb-8cb9-5a32d22c50bc.PNG)

We decide to choose 5 and 7 clusters for modelling and the results are displayed below

![Capture4](https://user-images.githubusercontent.com/32663193/122119407-25d0f700-cdf7-11eb-85af-f30a89e0f5e1.PNG)

Looking at this graph we understand that:

1. people who make around 40-70K a year tend to have a spending score between 40-60
2. people who make around 15-40K and 70-140K a year tend to have a spending score that is less than 40 or greater that 60

![Capture5](https://user-images.githubusercontent.com/32663193/122119421-29fd1480-cdf7-11eb-85e2-d2e1c1c1063a.PNG)


Looking at this graph we understand that:

1. people who make around 40-70K a year tend to have a spending score between 40-60
2. people who make around 15-40K and 70-140K a year tend to have a spending score that is less than 40 or greater that 60
3. we can afford to not focus too much on people who make more that 100K a year since there aren't a lot of people in these clusters
4. while each cluster with an income of less than 100K seem to be the same size, the purple cluster seems just as dense as the yellow and light green cluster combined. Similarly the purple cluster seems just as dense as the teal and green cluster combined

we can that in visually speaking, equal amounts of people shopping with incomes between 15-40K, 40-70K and 70-90K.

similarly we can say that we have equal amounts of people shopping with a shopping score between 0-40, 40-60 and 60-100.
While originally I thought 5 clusters would be good enough, 7 clusters seem to give more information.<br>

For GMM we looked at the AIC and BIC and decide to try 5 and 8 clusters.

![Capture6](https://user-images.githubusercontent.com/32663193/122119890-bd364a00-cdf7-11eb-88af-a712ac7826ef.PNG)

After looking at the 5 and 8 cluster GMM, we decided to ignore the 8 cluster GMM as it looks a bit messy

![Capture7](https://user-images.githubusercontent.com/32663193/122120184-1aca9680-cdf8-11eb-9fe6-41909ad45c56.PNG)
![Capture8](https://user-images.githubusercontent.com/32663193/122120190-1c945a00-cdf8-11eb-8750-fe6b66efb8e3.PNG)


I prefer GMM with 5 clusters rather than GMM with 8 as the clusters more easily and just as accurately translates to categories. 
While I prefer the visuals from the K-Means graphs, the GMM visuals show us a more accuracy bounding box over our data. 
If we focus on the short and medium radius for each cluster, we can make some general rules by turning the radii into lines/vectors.

## Conclusion

Looking at each cluster from GMM with 5 clusters we can make the following assumptions/suggestions:

- blue: <br> 
  low income, high spenders <br> 
  vector: vertical <br> 
  We should remember that this category spends a lot of money, this means they are happy with what we have already.

- yellow: <br> 
  low income, low spenders <br> 
  vector: vertical <br> 
  This category either cannot find products of interest or cannot afford them, probably the former due to the blue cluster having the same income. The mall can either try incorporating new stores that does not sell expensive items or create targeted ads for this category. <br> 

- purple: <br> 
  mid income, mid spenders <br> 
  vector: sloped down (m = -1) <br> 
  This category already generates profits but not at a high rate. While this category has the lowest concerns, perhaps a rewards program may incentivize them to buy a bit more. <br> 

- dark green: <br> 
  high income, high spenders <br> 
  vector: horizontal <br> 
  We should remember that this category spends a lot of money, this means they are happy with what we have already. <br> 

- light green: <br> 
  high income, low spenders <br> 
  vector: sloped up (m = 0.4) <br> 
  This category can afford expensive products but doesn't buy anything at our location. Perhaps the introduction of a popular luxurious brand into the mall may boost spending scores within this category. There are high income customers who spend a lot so maybe by analyzing them a bit more, we can incentivize this category <br> 
