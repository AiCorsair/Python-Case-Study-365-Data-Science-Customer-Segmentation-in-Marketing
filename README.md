# Python Case Study: 365 Data Science Customer Segmentation in Marketing


## Table of Contents

- [I. Introduction](#I.-Introduction)
- [II. Key Questions](#II.-Key-Questions)
- [III. Exploratory Data Analysis](#III.-Exploratory-Data-Analysis)
- [IV. Hierarchical & K-Means Clustering](#IV.-Hierarchical-&-K-Means-Clustering)
- [V. K-Means Model Assessment](#V.-K-Means-Model-Assessment)
- [VI. Key Visualizations & Tables](#VI.-Key-Visualizations-&-Tables)
  - [1. Hierarchical Dendrogram & K-Means Elbow Method](#1.-Hierarchical-Dendrogram-&-K-Means-Elbow-Method)
  - [2. Correlation of CLV with Regions & Channels](#2.-Correlation-of-CLV-with-Regions-&-Channels)
  - [3. Bar Plots of Minutes Watched & CLV by Cluster](#3.-Bar-Plots-of-Minutes-Watched-&-CLV-by-Cluster)
- [VII. Marketing Strategy Recommendations](#VII.-Marketing-Strategy-Recommendations)
  - [1. Facebook Campaigns](#1.-Facebook-Campaigns)
  - [2. YouTube Influencers Strategy](#2.-YouTube-Influencers-Strategy)
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

### 1. Hierarchical Dendrogram & K-Means Elbow Method

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

- As we can see, the correlation of CLV is highest with the region groups: English-Speaking Countries, Western Europe, and Other Countries.

- Interestingly, CLV is highly negatively correlated with countries from the rest of the world (**-0.9075**). This is likely because these countries include developing nations with lower incomes, and their students tend to seek cheaper or free data science education alternatives.


### 3. Bar Plots of Minutes Watched & CLV by Cluster

![Bar Plots](https://github.com/user-attachments/assets/c81a94eb-7420-4e3b-8165-fa286fa38a8d)

The number of minutes watched ranges from `1,165.42` to `2,767.64` (median is `1,816.31` mins), while the customer lifetime value ranges from `95.79` to `144.03` (median is `122.17`).

- **Cluster 0 (7.98%):** Students from Facebook, mainly from the rest of the world, have the highest number of minutes watched and below average CLV.

- **Cluster 1 (37.58%):** The largest cluster, with students from mixed regions, mainly from YouTube, has average minutes watched and CLV.

- **Cluster 2 (4.62%):** The smallest cluster, with students who joined through friends, mainly from English-speaking countries and Western Europe, has the highest CLV and above-average minutes watched.

- **Cluster 3 (4.93%):** Students from English-speaking countries (US, Canada, UK, Australia) and LinkedIn have the lowest minutes watched and average CLV.

- **Cluster 4 (17.5%):** Students from mixed regions who discovered the platform via Google have average minutes watched and CLV.

- **Cluster 5 (7.85%):** Students referred by friends, from the rest of the world, have the lowest CLV and below-average minutes watched.

- **Cluster 6 (12.02%):** Students mainly from the rest of the world, who joined via LinkedIn, have below-average minutes watched and CLV.

- **Cluster 7 (7.51%):** Students from mixed regions who joined through other channels have above-average minutes watched and average CLV.


## VII. Marketing Strategy Recommendations

After identifying the customer segments, we can now discuss the results with the marketing team to implement targeted strategies. It’s noteworthy that 365 Data Science has equal spending budgets across the three region groups.


### 1. Facebook Campaigns

- For campaigns targeting Facebook users, we recommend personalized ads or discounts to increase CLV. As `Cluster 0` is mainly from the rest of the world, 365 Data Science Facebook posts should be tailored to maintain high engagement and encourage higher spending overall.

- Given that this segment has fewer students from English-speaking countries or Western Europe, it would be worth exploring how focusing more on similar audiences on Facebook could impact the results, especially since students from the rest of the world tend to have the lowest CLV.


### 2. YouTube Influencers Strategy

- To leverage 365 Data Science's popularity on YouTube, we recommend collaborating with influencers (experts in AI and data science) to create high-quality, in-demand video content that resonates with people from various regions. These influencers can also promote courses they create for 365 Data Science to attract new customers and boost spending.

- Since `Cluster 1` is from mixed regions, it may be more effective to focus efforts on targeting YouTube audiences from English-speaking countries or Western Europe, where students typically have a higher CLV.


### 3. Google Campaigns

- We can design Google-based campaigns targeting people from English-speaking countries and Western Europe, with region-specific ads that align with their preferences and interests.

- Additionally, offering personalized discounts or exclusive access to tailored content will likely boost engagement and CLV by catering to their regional needs.


### 4. LinkedIn Content Strategy

- For LinkedIn users, especially from English-speaking countries, we can tailor content focusing on professional development and educational growth for both career switchers and students. Making special offers and addressing major pain points can attract new customers and boost spending.

- It's important to note that most 365 Data Science students from LinkedIn are not from Western Europe. This presents an opportunity to explore how targeting Western Europeans could impact engagement and CLV.


### 5. Referral Program Enhancement

- We recommend enhancing the referral program by offering discounts or bonuses to both referrers and new students. Highlighting successful referral stories can motivate others to participate, creating a viral effect and boosting overall engagement and spending.

- Interestingly, students referred by friends from the rest of the world have the lowest CLV and below-average minutes watched. Therefore, focusing more on English-speaking countries and Western Europe, where referral success and CLV are higher, would be more effective.


### 6. Alternative Channels Strategy

- We can target audiences from alternative channels with professional development and educational growth content, addressing common pain points, and identifying the posts that generate the most engagement.

- Once we’ve pinpointed effective posts, we can create personalized offers and discounts to attract new customers, tapping into new opportunities and engaging students on less common platforms.

- Since students from the rest of the world have lower CLV, shifting focus to higher-value segments and investing less in regions with lower ROI would be more effective.
