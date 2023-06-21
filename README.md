# AirBnB in NYC: Accommodation Segmentation

![Alt text](AirBnB-in-NYC-Accommodation-Segmentation/Screenshot 2023-06-21 at 12.34.09.png)

### Table of Contents
- [Project Description](#project-description)
- [Dataset](#dataset)
- [Approach](#approach)
- [Data Preprocessing](#data-preprocessing)
- [Exploratory Data Analysis](#exploratory-data-analysis )
- [Accommodation Segmentation](#accommodation-segmentation)
- [Results and Insights](#results-and-insights)
- [Conclusions](#conclusions)


## Project Description
The goal of this project is to segment and analyze the AirBnB accommodations in New York City (NYC) based on their characteristics and attributes. By analyzing the dataset, I aim to gain insights into the different types of accommodations available in NYC and understand the factors contributing to their pricing and popularity. This analysis can be valuable for both AirBnB hosts and potential guests in making informed decisions.

## Dataset
The dataset used in this project is sourced from Kaggle's AirBnB listings in NYC dataset. It includes information about various accommodations in NYC, such as listing details, location, availability, pricing, and reviews. The dataset provides a rich source of information for performing the segmentation analysis.

## Approach
The project follows the following approach:
1. __Data Preprocessing__: The raw dataset is processed and cleaned to handle missing values, outliers, and inconsistencies. Relevant features are selected for the segmentation analysis.
2. __Accommodation Segmentation__: Using unsupervised learning techniques such as clustering, the accommodations are grouped into segments based on their attributes. This allows us to identify distinct patterns and similarities among accommodations.
2. __Results and Insights__: The segmented accommodations are analyzed to uncover insights related to pricing, popularity, location, and other relevant factors. Visualizations and statistical summaries are used to present the findings.

## Data Preprocessing
Before performing the segmentation analysis, the dataset undergoes preprocessing steps such as:
1. __Handling missing values__: Missing values are removed from the dataset. Among the columns, last_review and reviews_per_month have the highest number of missing values (n=10052). These columns are excluded from the analysis as the missing values are likely an indication that the accommodations were not yet rented to a guest. Additionally, the columns host_name and name have a few missing values (21 and 16 respectively), and they are also removed from the dataset as they do not provide any meaningful information for the segmentation process.
2. __Outlier detection__: To ensure accurate clustering, outliers in the numerical features were identified and subsequently removed. Outliers can have a substantial impact on the clustering process, as they can skew the distribution and influence the clustering algorithm's results. By removing outliers, we aim to enhance the robustness and reliability of the clustering analysis.

   | Column name   | n outliers |
   | ------------- | -------------       |
   | price  | 2077  |
   | minimum_nights  | 4270  |
   | number_of_reviews  | 3310  |
   | calculated_host_listings_count  | 2878  |
   
4. __Feature selection__: Relevant features for the segmentation analysis are chosen based on their significance and potential impact.

## Exploratory Data Analysis 
The exploratory analysis of the AirBnB accommodations dataset uncovered several interesting insights about its structure, patterns, and relationships:
1. The majority of listed AirBnB accommodations are located in Brooklyn and Manhattan, indicating the popularity of these areas among hosts.
2. Shared rooms constitute only a small portion of the listed apartments, suggesting that most hosts prefer renting out entire apartments or private rooms.
3. It was observed that entire apartments tend to be more expensive than private rooms, and private rooms are generally pricier than shared rooms.
4. Accommodations in Manhattan appear to have higher average prices compared to other areas, reflecting the premium nature of this location.
5. A moderate positive correlation was found between the price per night and the type of accommodation, indicating that certain types of accommodations command higher prices. 6. Additionally, there was a negative correlation between the price per night and the longitude, suggesting that accommodations located further west tend to have lower prices.

These findings provide valuable insights into the distribution and pricing dynamics of AirBnB accommodations in NYC, setting the stage for further analysis and clustering of the dataset.

## Accommodation Segmentation
In the clustering stage of the analysis, I employed unsupervised learning techniques, specifically clustering algorithms like K-means clustering, to segment the AirBnB accommodations. By selecting relevant features, I aimed to group similar accommodations together, enabling the identification of common characteristics and patterns within each segment.

To determine the optimal number of clusters, I utilized the __elbow method__, which involved plotting the within-cluster sum of squares (WCSS) against the number of clusters. Based on the plot, I determined that five clusters would be appropriate for our analysis.

Before performing the clustering, I applied feature scaling to ensure that all variables were on a similar scale. This was done using the `StandardScaler()` function, which standardized the features by removing the mean and scaling to unit variance. Scaling the data helps in avoiding any bias caused by variables with different units or ranges.

By applying these techniques, I aimed to uncover distinct groups and patterns within the AirBnB accommodations dataset, providing valuable insights for further analysis and decision-making.

## Results and Insights
The segmention revealed the following patterns:
1. Cluster-0 primarily comprises private rooms located in Manhattan and Brooklyn. This cluster represents a popular choice for travelers seeking more affordable accommodation options within these areas.
2. Cluster-1 is characterized by high-priced entire home/apartments situated in Brooklyn. With an average price of $150 per night, this cluster caters to individuals or groups seeking a more luxurious and exclusive stay experience.
3. Cluster-2 consists of accommodations that have received a significant number of reviews, with an average of more than 50 reviews. Additionally, these accommodations are available for an average of 150 days per year, indicating their popularity among guests.
4. Cluster-3 represents accommodations with a high calculated host listing count, averaging 2.5 listings per host. These accommodations are available for an average of 160 days per year, suggesting that hosts in this cluster actively manage and rent out multiple properties.
5. Cluster-4 comprises accommodations with extended stays of five nights or more. This cluster caters to guests who require longer-term accommodations and offers a suitable option for those seeking an extended visit to New York City.

By examining the characteristics of each cluster, we gain valuable insights into the diverse offerings and preferences within the AirBnB accommodations in NYC. These insights can aid in understanding market trends, tailoring marketing strategies, and providing personalized recommendations for potential guests.

### Natural language processing
Each cluster was assigned a name by analyzing the names that homeowners have given their Airbnbs and examining the text features used in their home advertisements. By observing how individuals advertise their homes and the creative names they use, we were able to derive distinct and descriptive names for each cluster. This approach adds a unique and personalized touch to the clustering results, allowing us to better understand the characteristics and offerings of each segment.

#### Sentiment analysis
I conducted an analysis of the descriptions provided by the owners for their listed accommodations. To gain insights into the sentiment expressed in these descriptions, I utilized the `SentimentIntensityAnalyzer()` and the `vader_lexicon`. Surprisingly, I discovered that a number of descriptions were classified as negative, which was unexpected as I anticipated a majority of them to be positive or neutral. This finding adds an interesting dimension to the dataset and prompts further exploration into the factors contributing to the negative sentiment expressed in these descriptions.

   | Cluster   | negative | neutral | positive | 
   | -------- | -------- | -------- | -------- | 
   | 0	| 146	| 2894	| 3850 |
   | 1	| 148	| 3346	| 3913 |
   | 2	| 115	| 1792	| 2351 |
   | 3	| 64	| 1335	| 1853 |
   | 4	| 76	| 2103	| 2298 |
   | __TOT__ | 549 |	11470	| 14265 |

#### Words frequency
After eliminating stopwords from the text data, I examined the frequency of the top 25 most frequently used words in each cluster. Additionally, I identified the most common adjective used within each cluster. By doing so, I aimed to gain a better understanding of the language patterns and themes present within each cluster. This analysis allowed me to assign a representative adjective to each cluster, providing further insights into the distinguishing characteristics of the accommodations within each segment.

## Conclusions
By performing accommodation segmentation and analyzing the AirBnB dataset, we gain valuable insights into the different types of accommodations in NYC. This analysis can help both hosts and guests make informed decisions by understanding the factors influencing pricing, popularity, and customer satisfaction. The findings can also be used to improve marketing strategies, optimize pricing, and enhance the overall guest experience in the AirBnB ecosystem.




Feel free to explore the code and adapt it to your specific requirements. Enjoy analyzing the AirBnB accommodations in NYC and discovering valuable insights!
