# ETL Pipeline: COVID-19, education, and unemployment dataset

ETL pipeline to clean, merge, and export data into a SQL database. 

## Description

## Extract
Datasets on COVID-19 positivity and death rates, education levels, and unemployment rates in the United States were 

Extracting the datasets was fairly simple. The data was in CSV format, so we created a Jupyter Notebook file and loaded the CSV files into it in order to prepare the data for cleaning.

## Transform
- Unemployment data
  -	As previously stated, the unemployment data included figures from 2000-2019. In order to prep the data for inclusion in our SQL database, I used the Jupyter Notebook interface to drop the majority of the columns from this dataset so that we only have relevant data from 2019. 
  -	I removed 87 irrelevant columns from the dataset. The data was very clean, so there was minimal cleaning to do otherwise.

- COVID-19 data
  -	The “geoid” column, which contained “USA-#####” values, was split on the “-” and data was stored in two new columns. The column containing “USA” values was dropped and the column containing numerical values was stored as “FIPS_Code.” The FIPS_Code column was used to merge with the other two datasets. 
  -	The “FIPS_Code” column data type was converted from object to integer to prepare for merging. 
  -	The “county” and “state” columns were converted from object to string for the groupby function
  -	The DataFrame was grouped by “FIPS_Code” and the aggregate function was used to store the first county and state name of each group, and to calculate the sum of average cases and average depths per 100k (average deaths and average cases columns were dropped in this step)
  -	The index was reset before exporting the cleaned DataFrame as a csv file
 - Education data
    -	This dataset was transformed from 48 columns to 6 columns
    -	FIPS Code and state columns were kept for merging
    -	Columns with percent of adults with less than a high school diploma, only a high school diploma, comploeted some college, and completed a bachelor's degree or high from 2015-2019 were kept.

## Load
We created a local SQL database called "Project 2." Within this database, we created three tables and imported our cleaned dataframes from Pandas, assigning the FIPS_Code as the primary key in each table.

We chose this topic because it was something that we felt was topical, and general enough that we might be able to build on in the future with additional datasets. Additionally, we feel that if we were to dig a bit more into the data, we could extrapolate some trends from our final dataset.

![image](https://user-images.githubusercontent.com/74067302/140006516-782eb396-fc9a-480e-99ad-94799a18912b.png)

## Data Sources
- COVID-19 
  - "The New York Times. (2021). Coronavirus (Covid-19) Data in the United States. Retrieved [Insert Date Here], from https://github.com/nytimes/covid-19-data." (CSV) 
- Education
  -  "County-level Data Sets." USDA Economic Research Service, US Department of Agriculture. Access date: Sept 8, 2021. URL: https://www.ers.usda.gov/data-products/county-level-data-sets/ (CSV file)
- Unemployment
  - "USA Unemployment & Education Level" Kaggle.com. Access date: October 30, 2021. https://www.kaggle.com/valbauman/student-engagement-online-learning-supplement/version/3?select=unemployment.csv

  
