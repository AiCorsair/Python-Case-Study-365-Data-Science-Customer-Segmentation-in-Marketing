# Python Case Study: 365 Data Science Customer Segmentation in Marketing


## Table of Contents

- [I. Introduction](#I.-Introduction)
- [II. Key Questions](#II.-Key-Questions)
- [III. Exploratory Data Analysis](#III.-Exploratory-Data-Analysis)
- [IV. Hierarchical & K-Means Clustering](#IV.-Hierarchical-&-K-Means-Clustering)
- [V. K-Means Model Assessment](#V.-K-Means-Model-Assessment)
- [VI. Key Visualizations & Tables](#VI.-Key-Visualizations-&-Tables)
  - [1. Hierarchical Clustering & K-Means Elbow Method](#1.-Hierarchical-Clustering-&-K-Means-Elbow-Method)
  - [2. Correlation of CLV with Regions & Channels](#2.-Correlation-of-CLV-with-Regions-&-Channels)
  - [3. Bar Plots of Minutes Watched & CLV by Cluster](#3.-Bar-Plots-of-Minutes-Watched-&-CLV-by-Cluster)
- [VII. Marketing Strategy Recommendations](#VII.-Marketing-Strategy-Recommendations)
  - [1. Facebook Campaigns](#1.-Facebook-Campaigns)
  - [2. YouTube Campaigns](#2.-YouTube-Campaigns)
  - [3. Google Campaigns](#3.-Google-Campaigns)
  - [4. LinkedIn Content Strategy](#4.-LinkedIn-Content-Strategy)
  - [5. Referral Program Enhancement](#5.-Referral-Program-Enhancement)
  - [6. Alternative Channels Strategy](#6.-Alternative-Channels-Strategy)


## I. Introduction

In this project, we analyzed real-world customer data from an onboarding survey for the 365 Data Science platform to perform customer segmentation. This is critical for businesses to understand customer behavior and develop personalized marketing strategies.

The project included data cleaning, exploration, feature engineering, clustering algorithms implementation, and results interpretation. We applied two widely used clustering techniques: **K-Means** and **Hierarchical Clustering**.

The analysis segmented a sample of over `3,800` members (representing the entire population) to identify trends like acquisition channels and geographic influences. These insights will assist the marketing team in prioritizing resources during campaigns.

The `Customer_Data.csv` file includes:

- **minutes_watched:** Total minutes a student watched since joining.

- **CLV:** Average revenue a customer generated over their lifetime (in USD or EUR, currency uncertain).

- **region:** `0` for English-speaking countries (USA, Canada, UK, Australia), `1` for Western Europe, and `2` for other countries.

- **channel:** The source through which the customer learned about the 365 program (e.g. Google, LinkedIn).


## II. Key Questions

- Are there specific geographical locations or acquisition channels where students predominantly discover the 365 Data Science platform?

- How are geographic locations and acquisition channels connected to student engagement and spending?


## III. Exploratory Data Analysis

- We loaded and previewed the customer data, generated summary statistics, displayed column data types, and counted the missing values. Null values in the ‘minutes_watched’ column were replaced with `0`, as these students purchased the program but had not watched any video content.

- We computed the correlation matrix for numerical columns and visualized it using a heatmap. Additionally, we created a scatter plot to examine the relationship between 'minutes_watched' and 'CLV'.


## IV. Hierarchical & K-Means Clustering

- We converted the categorical columns ('region' and 'channel') into dummy variables, automatically replacing the original columns. Additionally, we renamed all columns for better readability and scaled the data.

- We performed hierarchical clustering using the Ward method and plotted a dendrogram to visualize the results.

- We calculated the Within-Cluster Sum of Squares (WCSS) for various cluster counts in K-means and used the Elbow Method plot to identify the optimal number of clusters.


## V. K-Means Model Assessment

- We applied K-means with `8` clusters and assigned cluster labels to ‘customers_kmean’ (a copy of the original ‘customers’ DataFrame).

- For the ‘customers_grouped’ variable, we grouped customers by cluster, calculated cluster size and proportion, and summarized the data with mean values.

- We renamed clusters for better interpretation (e.g. “Facebook-Centric, Highest Minutes Watched” instead of `0`) in ‘customers_grouped’ and set the index name to 'Cluster Label.'

- We created side-by-side horizontal bar plots to visualize 'Minutes Watched' and 'CLV' by cluster. Afterward, we created two scatter plots: one for original 'CLV' vs. 'Minutes Watched' and another for scaled 'CLV' vs. 'Minutes Watched' (without outliers).


## VI. Key Visualizations & Tables

### 1. Hierarchical Clustering & K-Means Elbow Method

![Dendrogram   Elbow](https://github.com/user-attachments/assets/fab6ec7f-2426-4fbe-86bd-71a9172f3f3f)

- The hierarchical clustering results identified `8` distinct clusters, providing a recommended cluster count based on the data.

- The K-means Elbow Method suggested `7` clusters, differing from the `8` clusters found through hierarchical clustering.

- As a result, we chose the hierarchical clustering results and performed K-means clustering with `8` clusters.


### 2. Correlation of CLV with Regions & Channels

| Variable                       | Correlation with CLV |
|--------------------------------|----------------------|
| **English-Speaking Countries** | 0.7912               |
| **Western Europe**             | 0.6179               |
| **Other Countries**            | -0.9075              |
| **Google**                     | 0.0881               |
| **Facebook**                   | -0.2462              |
| **YouTube**                    | 0.1832               |
| **LinkedIn**                   | -0.2121              |
| **X**                          | 0.1832               |
| **Instagram**                  | 0.1832               |
| **Friend**                     | 0.0853               |
| **Other**                      | 0.1409               |

As we can see, the correlation of CLV is highest with the region groups: English-Speaking Countries, Western Europe, and Other Countries. Interestingly, CLV is highly negatively correlated with countries from the rest of the world (**-0.9075**). This is likely because these countries include developing nations with lower incomes, and their students tend to seek cheaper or free data science education alternatives.


### 3. Bar Plots of Minutes Watched & CLV by Cluster


