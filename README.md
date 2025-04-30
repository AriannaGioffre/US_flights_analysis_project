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

#### Exploratory analysis
We analysed in total 28 millions of flights with a fare range between 67$ and 465$, a max delay of 141 min and 10 different airlines.

In the picture below it is possible to observe the trend 
![image](https://github.com/user-attachments/assets/883ec481-5bbf-4720-bf99-8e97553efd55)




