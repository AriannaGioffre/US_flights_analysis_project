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

We analyzed the relationship between different features and we could conclude that:
1. There is no correlation between `distance` and `delay` (Pearson correlation value of 0.0064) - higher distance does not encourage higher delays 

![image](https://github.com/user-attachments/assets/1fecdc4d-1a53-4a8e-9754-14f0683c9fe0)

2. There is small correlation between `fare` and `delay` (correlation value 0.1057)

![image](https://github.com/user-attachments/assets/5dbb51f8-dd5e-4907-8c81-248f70ced56d)

5. There is high correlation between `distance` and `fare`
   - <b>A/B Testing</b> with a <b>t-test</b> to compare the means of cheap and expensive group
     <div><b><font style="font-size: 18px;" face="Quicksand">H0:&nbsp;</font></b></div><font style="font-size: 18px;" face="Quicksand"><div style=""> There is no difference in the mean far of the two groups
   
     <div><b><font style="font-size: 18px;" face="Quicksand">Results:&nbsp;</font></b></div><font style="font-size: 18px;" face="Quicksand"><div style="">Lower mean for close flight group;&nbsp;</div><div style="">p-value 0&nbsp; &gt;&gt; H0 can be rejected</div></font>

   - <b>Correlation Test </b>and <b>LInear Regression Model</b>

     <div><b><font style="font-size: 18px;" face="Quicksand">Results:&nbsp;</font></b></div><font style="font-size: 18px;" face="Quicksand"><div style="">Correlation of 0.5426 indicating a moderate positive correlation&nbsp;</div><div style="">R²: 0.294&gt;&gt; only 29.4% of fares can be explained by distance</div><div style="">p-value 0 &gt;&gt; R2 is statistically significant</div><div style="">Coefficient: 0.0557</div></font>

![image](https://github.com/user-attachments/assets/7755a752-3fa9-4819-b6dc-26cfa09f8722)

7. There is strong statistical difference in the distribution of `delay` between different `airline price category`
8. There is strong statistical difference in the distribution of `fare` between different `destination/origin regions`
9. There is strong statistical difference in the distribution of `delay` between different `air traffic conditions`
   

