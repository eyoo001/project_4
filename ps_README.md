# Predicting the Spread of West-Nile Virus Mosquitos in Chicago
## by Eric Yoo, Romand Tse, Perry Shyr

   We propose to reduce the human infection rate of West-Nile virus as transmitted by C.Pipiens and C.Restuans mosquitos in the vicinity of Metropolitan Chicago via larvicide in fewer strategic locations based on a logistic-regression model based on data provided by the city. We use the ROC-AUC as the primary metric for success, noting that the data is dependent on time.

### Executive Summary:

   West Nile Virus continues to be a problem in the United States since it’s first report in 1999.  By the end of 2002, Illinois had counted 884 cases and 67 deaths.  During 2017, Illinois counties (63) reported WNV positive cases, including 90 human cases, and 8 deaths.
   Our solution is to proactively control the concentration of the mosquito population and thereby minimizing the human infection rate of the virus.  We use a time-dependent predictive model to identify and mosquito-prone areas around Chicago.  From these results, we can target these areas with larvicide and minnow-seeding as the most cost-effective strategy for limiting virus transmission.

## Contents

| Notebook | Description |
| --- | --- |
| 1 | Preprocessing |
| 2 | Data-exploration |
| 3 | Modeling |
| 4 | Model Evaluation |


### Findings
#### Weather Data:
a) Stations are located at O'Hare and Midway Airports.
b) "M" is for missing data; most if not all from Station-2.
c) Recordings begin on May-01-2007 and end on Oct-31-2014, covering 1,472 days.
d) The positive-class of mosquitos infected with West-Nile virus greatly under-represented (unbalanced).
e) The Culex Pipiens species was a stronger transmission vector than the predominant Culex Restuans.
f) C.Restuans accounted for a greater percentage of mosquitos caught earlier in the summer.
g) There was a roughly 21-day lag between mosquito concentration and virus presence during any given year.
h) Mosquito concentraion and virus presence overall across multiple years tended to peak in August.
i) ROC-AUC scores were higher-performing for the mixed C.Pipiens/C.Restuans, than for the separate species.
j) The classification threshold of 0.47 seemed to be the optimal trade-off between false-negatives and false-positives.


### Research
   
   We cite two sources for our understanding of virus transmission between host and vectors:
https://news.wisc.edu/west-niles-super-spreader-how-about-the-american-robin/ and 
https://wwwnc.cdc.gov/eid/article/12/3/05-1004_article.


# Summary of Methodology and Results

#### Cleaning and Pre-processing of Data

   We imputed values for missing data in the 'Tavg', 'PrecipTotal', 'AvgSpeed', 'WetBulb', 'StnPressure', 'SeaLevel', 'Heat' and 'Cool' in the form of "M" and "  T" values.  Most missing values were found in Station-2 data.  We suggested that feature-columns 'Depth' and 'Water1' could be ignored or deleted.
   New derived features were added for year-squared and month-squared to model the time-dendent.  These may have been stronger predictors than the weather-related features.

#### Data exploration in association with Modeling

   The distribution of weather data was plotted and indicated apparent time-dependence patterns between the odd-numbered years.  We found weak correlations between temperature, pressure and wind-speed and mosquito concentration and/or West-Nile virus presence.  The coverage and timing of the spraying patterns appear to lag virus presence by at least a week, suggesting that spraying was reactionary, rather than prevatative.

#### Detailing the Two Classification Models using Logistic-Regression and CaRT Models

| CaRT's |  |
| --- | --- |
| Mode-1 | 0.81 |
| Model-2 | 0.85 |
| Average | 0.83 |


| Log-Reg |  |
| --- | --- |
| Test | 0.93 |
| Test | 0.85 |
| Average | 0.89 |


#### Statistical Metrics to Evaluate the Models

   We use the Receiver-operator Characteristic-AUC metric to evaluate our models.

| CaRT's | ROC-AUC |
| --- | --- |
| Model-1 | 0.92 |
| Model-2 | 0.85 |
| Average | 0.89 |


| Log-Reg | ROC-AUC |
| --- | --- |
| Test | 0.85 |
| Test | 0.77 |
| Average | 0.82 |


#### Conclusion

   A logistic-regression model for predicting the spread of the mosquito population serves as the basis of a cost-effective solution to infection-rate control in Chicago.  We expect that setting a threshold for our evaluation metric (ROC-AUC) of about 0.47 will result in the optimal balance of false-negatives and false-positives.  With more contiguous multi-year data, this model can be tuned to a higher degree.
   
   This model can be used to drive a multi-pronged virus-control campaign including coordinated larvicide, minnow-seeding and aerial-/strategic-spraying efforts.  Weather plays a key role in the proloferation of the mosquito population, but our time-dependence modeling can direct us towards efficient counter-measures in the right locations.
   
   The projected cost of this campaign, at close to the current budget of $1.7m, throughout the months of July and August is our best chance to curb the enormous burden caused by West-Nile virus infection.


# Appendix

### Data-file Contents:

#### CSV-type

| Name | Description |
| --- | --- |
| weather.csv | Weather data from two separate airport-recording stations, from 2007 to 2013. |
| train.csv | Data from mosquito-trap collection for odd-numbered years between 2007 and 2013. |
| test.csv | Model-testing file by species, date and possible locations. |
| spray.csv | Adulticide-spraying data from 2011 and 2013 during the summer months of June-September. |
| smapleSubmission.csv | The populated test file submitted for the Kaggle competition. |
| ps_weather_processed.csv | The cleaned weather-data file with date-indexed rows. |
| bullshit.csv |  |


#### Other-type

| Name | Description |
| --- | --- |
| noaa_weather_qclcd_documentation.pdf | Data dictionary for the weather-related data. |
| mapdata_copyright_openstreetmap_contributors.txt | Open-source mapping coordinates file. |
| mapdata_copyright_openstreetmap_contributors.rds | Associated mapping reference file. |
| eda.html | Bokeh-visualization for exploratory data analysis. |








