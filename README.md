# 🛫US Flight Analysis
This project focuses on analyzing flight data across the United States to uncover patterns and trends in domestic air travel. The ultimate aim is to enrich flight comparison platforms by offering delay predictions and fare benchmarks to enhance user decision-making.

## 📊 Project Overview
The US Flight Analysis project includes:

1. Exploration of three large-scale flight datasets, totaling over 28 million rows
2. Comprehensive data cleaning and preprocessing 
3. Analysis of delay patterns by airline, airport, regions and weather conditions 
4. Statistical testing to uncover correlations and significant differences, using linear regression, correlation analysis and the Kruskal–Wallis H test
5. Development of two clustering models to categorize flights based on selected features
6. Implementation of predictive models for fares and delays using Random Forest Regression
7. Creation of interactive dashboards with Looker Studio to present key findings
8. Identification of performance insights and optimization opportunities

## 📂 Dataset
Three different data sources from Kaggle have been used for the projecs:
1. [Flight Status Prediction](https://www.kaggle.com/datasets/robikscube/flight-delay-dataset-20182022?select=Combined_Flights_2018.csv) 
   Includes 6 datasets with a total of 61 columns and approximately 29 million rows (2018–2022).
3. [US Airline Flight Routes and Fares](https://www.kaggle.com/datasets/bhavikjikadara/us-airline-flight-routes-and-fares-1993-2024)
   Contains 23 columns and about 245,000 rows, offering detailed fare and route information (1993–2024).
5. [US Weather Events](https://www.kaggle.com/datasets/sobhanmoosavi/us-weather-events)
   Comprises 14 columns and around 6 million rows, covering significant weather events across the US

These datasets collectively provide information on airports, airlines, routes, delays, fares, and weather conditions—key features for the analysis and predictive modeling performed in this project.

## 🧪 Methodology
The first step involved cleaning and preparing the datasets using BigQuery:

1. Identified and handled null values, removing them when necessary
2. Determined primary keys for each table to ensure data integrity
3. Cast columns to appropriate data types (e.g., DATE, INTEGER)
4. Merged datasets from different years into a single unified table
5. Split "coordinates" columns into separate latitude and longitude fields
6. Applied additional transformations to facilitate grouping and joins, such as creating a Year-Quarter column for easier time-based aggregation

#### 📈 Exploratory analysis
We analyzed a total of 28 million flights, with fares ranging from $67 to $465, a maximum recorded delay of 141 minutes, and flights operated by 10 different airlines.

The chart below illustrates the trend in the number of flights over the years, along with the distribution of punctuality. A significant drop in flight volume can be observed in 2020, due to the impact of the COVID-19 pandemic. This reduction also coincides with fewer delays, possibly because lower air traffic decreased the likelihood of flight disruptions.

![image](https://github.com/user-attachments/assets/883ec481-5bbf-4720-bf99-8e97553efd55)

The heatmap reveals a higher concentration of delays on the East Coast compared to other regions. This observation led us to further investigate the impact of weather conditions, using a third dataset, to explore potential correlations.
![Screenshot 2025-05-01 185354](https://github.com/user-attachments/assets/0dadb4bc-a70a-4a4f-8324-83bf3c3230c6)

#### 🔍 Key findings
1. No Correlation Between `Distance` and `Delay`
   - Pearson correlation: 0.0064 → Indicates no relationship; longer flights do not cause more delays 

![image](https://github.com/user-attachments/assets/1fecdc4d-1a53-4a8e-9754-14f0683c9fe0)

2. Weak Correlation Between `Fare` and `Delay`
   - Pearson correlation: 0.1057

![image](https://github.com/user-attachments/assets/5dbb51f8-dd5e-4907-8c81-248f70ced56d)

5. Moderate Correlation Between `Distance` and `Fare`
   - Pearson correlation: 0.5426
   - A/B Testing (t-test): Compared mean fares between short- and long-distance flights.
     - H₀: No difference in mean fare between the two groups.
     - Result: Lower mean fare for shorter flights; p-value = 0 → H₀ rejected.
   - Linear Regression:
     - R² = 0.294 → Distance explains ~29.4% of fare variation.
     - Coefficient = 0.0557; p-value = 0 → Model is statistically significant.

![image](https://github.com/user-attachments/assets/7755a752-3fa9-4819-b6dc-26cfa09f8722)

7. Statistically Significant Difference in Delays by Airline Price Category
   - Airlines grouped by fare:
     - Low-cost (≤ $150)
     - Medium-cost (≤ $250)
     - High-cost (> $250)
   - Test: Kruskal-Wallis
   - Result: p-value = 0.009571 → Significant difference in delays across airline categories

![image](https://github.com/user-attachments/assets/3cc24f03-9689-494e-882b-0dbc881679bd)

9. Significant Difference in Fare Across Geographic Regions
   - Airports grouped into: West, Midwest, South, Northeast
   - Tests: ANOVA and Kruskal-Wallis
   - Result: p-value ≈ 0.000 → Fare varies significantly by region
     
![image](https://github.com/user-attachments/assets/1ec0adbe-30b6-41e2-a72e-88bcd5280dac)


11. Delay Strongly Affected by Weather Conditions
    - Tests: ANOVA and Kruskal-Wallis
    - Results:
      - H-statistic = 1612.51
      - p-value ≈ 0.000
        → Severe weather significantly increases delays

## 🔍 Feature Selection & Modeling Approach
Based on the results mentioned above, features that showed strong correlation or statistical difference have been selected to build predictive and clustering models.

#### 📊 Predictive Models Informed by Statistical Tests
1. Fare Prediction
   - Selected features:
     - distance
     - destination/origin regions
     - year + quarter
   - Model: Trees - Random Forest Regression
   - Model score: 0.9418
     
2. Delay Prediction
   - Features:
     - weather
     - destination/origin regions
     - air traffic
     - airline category
   - Model: Trees - Random Forest Regression
   - Model score: 0.8327
  

  

   

   

