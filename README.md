# Food Insecurity Analysis

## Problem Statement: 

How did the Washington, DC food desert landscape change between 2010 - 2019, and what inferences can we draw?

## Question to Answer:

Based on our findings, what recommendations can we make to help address key unresolved issues affecting food deserts more broadly, and how might we structure future research efforts to illuminate other possible trends? 

## Table of Contents: 
- Problem
- Data Acquisition & Methods
- Cleaning & EDA Notebook: 01_cleaning
- Geodata Notebook: 02_geodata
- Modeling Notebook: 03_modeling
- Results
- Conclusion
- Bonus: Modeling

## Software/Library requirements: 
- Python (3.9.12)
- Pandas (1.4.2)
- Numpy (1.21.6)
- Matplotlib (3.5.2)
- Seaborn (0.11.2)
- Scikit-learn (1.0.2)
- GeoPandas (0.10.2)
- Folium (0.12.1)
- Contextily (1.2.0)
- Openpyxl (3.0.9)

## Data Acquisition: 

We used the following five primary data sources to inform and guide our research efforts:

1. Food Access Research Atlas
Data extracted from the 2010 and 2019 Food Access Research Atlas included population data and related demographic data associated with every census tract in the United States based on 2010 Census determinations of those census tracts. Notably, these data sets provided census tract breakdowns using “low-income” and “low-access” definitions and estimates.\
Source: [USDA Economic Research Service](https://www.ers.usda.gov/data-products/food-access-research-atlas/download-the-data/)


2. Social Vulnerability Index
This data set ranked census tracks based on 15 social factors, including unemployment, minority status, and disability, in addition to other insights, such as educational attainment, housing type, transportation, etc.\
Source: [CDC - Social Vulnerability Index](https://www.atsdr.cdc.gov/placeandhealth/svi/at-a-glance_svi.html)

3. PLACES: Local Data for Better Health
Data assembled by the CDC that focuses on different measures of health across all census tracts in the United States, including health outcomes, prevention, health risk behaviors, and health status. Of note, this data set incorporates the results of various geocoded health surveys and links them to other types of socioeconomic data. \
Source: [CDC](https://chronicdata.cdc.gov/500-Cities-Places/500-Cities-Census-Tract-level-Data-GIS-Friendly-Fo/k86t-wghb)

4. SNAP Online
SNAP Online is an addition to the Supplemental Nutrition Assistance Program (SNAP) to allow SNAP benefits to be applied to online grocery purchases through authorized retailers. The program was created through the 2014 Farm Bill. \
Source: [USDA](https://www.ers.usda.gov/amber-waves/2021/july/online-supplemental-nutrition-assistance-program-snap-purchasing-grew-substantially-in-2020/)

5. Historical SNAP Retailer Locator Data
This link provides historical data on authorized SNAP retailers. This data is as of Dec. 31, 2021. The zipped CSV file includes retailer name, type, address, location, and authorization dates for retailers that were authorized to accept SNAP benefits at any point since 1990. \
Source: [USDA](https://www.fns.usda.gov/snap/retailer/historicaldata)
            

## Methods (Data Cleaning + Preprocessing): 

The data sources were not added to this repo on account of their size. When running the notebooks, we created a `datasets` folder in the main repo and stored our linked data files there.

The data sources used all contained high-quality data and there was little cleaning necessary. We only adjusted column names. Before we decided to focus on DC, we did notice that some census tracts had an unusually high population rate. We believe these tracts may be either an error or they may denote an unusual situation (e.g. military base, long-term healthcare facilities). If performing this analysis on other areas, we recommend removing these high-population census tracts. Our focus area of DC did not have this issue.  

We feature engineered four columns that indicate census tracts that 1) remained a food desert, 2) remained food accessible, 3) became a food desert, or  4) became food accessible using the existing column in both 2010 and 2019 datasets entitled ‘lilatract_1and10’, which was a binary identification on whether a census tract was or was not designated as a food desert with a 1-mile access definition. 

Only the 2019 dataset had information on tract demographics, so it was not possible to directly compare differences in demographics between 2010 and 2019. 

In addition to the USDA food desert information, we merged information from the CDC in the Social Vulnerability and PLACES datasets, which included health outcomes in Washington, DC. With this, we were able to compare health outcomes between food-accessible tracts and food deserts (e.g., data_2019_dc_CDC examines health and nutrition information of DC in 2019). See more in our output_data directory. 

To further investigate what happened inside food deserts in DC, we made use of the USDA’s authorized SNAP retailers dataset, which includes information about every retailer that is or was authorized, their location, type, and what dates they began and/or ended their authorization. 

## Results:

Comparing the listed authorized retailers within D.C. for the years 2010 and 2019 revealed a loss of fifteen retailers in total, which ranged from small grocery stores to supermarkets. Between 2010 and 2019, D.C. lost all of its medium grocery stores. There were huge shifts in the particular brands of retailers between these two years.

Despite efforts, food deserts slightly increased in the US overall between 2010 and 2019. In DC specifically, as noted in the analysis, three census tracts changed status from food desert to food accessible, six changed from food accessible to food desert, and six remained food deserts. 
Looking at the census tracts using the half-mile food desert measurement, the situation improved by 7% (61 food deserts reduced to 49 food deserts). However, when examining the 1-mile food desert measurement, the situation in DC actually worsened. When examining the poverty rates between 2010 and 2019 for these six tracts that changed to 1-mile food deserts, we did not find a significant change. This suggests that this area was designated a food desert because grocers actually moved away from those areas despite the heavy investment efforts. 

## Limitations: 

We had some trouble finding the data we wanted to explore because they were broken down by zip code or city/state instead of by census tract. This would give us a good overview, but not the granular view we were hoping to explore. 
We used the 2019 food desert data because that was the latest available information as of May 2022. This was a problem, since the census data was not updated until 2021, so we had to make do with census data for both 2010 and 2019. 
Our analysis is only focused on Washington, DC and cannot be generalized to other areas without significant reworking of the notebooks. 

## Conclusion & Recommendations: 

Our analysis suggests that despite over $1 billion put towards incentivizing grocery businesses to open in these areas, food deserts are still prevalent. Corporations have continued to consolidate, resulting in fewer locations for residents to access healthy foods. 

Even if these programs were successful and brought more grocers to food deserts, residents may still not have the funds to purchase healthy foods, since SNAP benefits provide on average $1.40 per person per meal. The high costs of healthy foods in most for-profit grocery stores would quickly wipe out a household’s SNAP benefits in just a couple of trips. 

Additionally, the way food deserts are defined may soon make the measure obsolete due to the prevalence of delivery options, but due to the cost constraints and that SNAP do not pay for delivery fees, increased access may still not change nutrition outcomes or food insecurity overall. 

For future efforts and policy improvements, we recommend the following:
Increase SNAP benefits per person and/or per household
Use public funds to invest in nonprofit grocers instead of for-profit businesses
Subsidize the costs of healthy foods for low-income areas

For future research efforts, we recommend shifting the focus away from food access and more on food affordability. 


## BONUS: Modeling

We fitted a Logistic Regression model to classify if a census tract is food-accessible or a food desert. Our feature matrix includes demographic features such as tractasian, and health features such as blood_pressure. We imputed missing values and standardized all features before fitting the model, which yielded an accuracy score of 93%, similar to the base model. While the model is not great in performance, the variable coefficients tell us which features are more important in the classification process. This allows us to gain a better understanding of food desert status‘ effects on the population. 


