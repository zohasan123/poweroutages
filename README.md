# Zoning Analysis and Predictive Modeling of Customers Affected in a Power Outage

### Created by Samuel Mahjouri and Zoya Hasan

# Introduction

Power outages pose significant risks to the safety, economy, and daily life of U.S. citizens, making it imperative to understand the factors that influence their duration and impact. Our  analysis utilizes a dataset on major power outage events in the continental U.S. from January 2000 to July 2016, provided by Mukherjee, Nateghi, and Hastak from Purdue University. The dataset includes information on geographical location, regional climatic conditions, land-use characteristics, regional electricity consumption patterns, and economic attributes of power outages in various states. Given such a holistic understanding of power outages, we posed the question that could support energy companies when considering where to aid during power outages. Our key question is: **What are the key factors that influence the durations of major power outages in the continental U.S., and how can these insights be used to mitigate future outages?** This question holds practical implications for utility companies, as well as regional communities. By identifying the determinants of outage durations, energy companies  can better prepare for and respond to future incidents. Given the increasing number and high severity of weather-related disruptions, understanding these dynamics, in correlation to power outages, is more critical than ever. The dataset used in this project has 1534 rows and 56 columns, and offers comprehensive insight to uncover our questions through data analysis. The dataset encompasses information on every major power outage in the United States from 2000 to 2016. Only a handful of columns were used for analysis and prediction, as described below:

Authors: **Samuel Mahjouri and Zoya Hasan**

***

| Feature        | Description     |
|:-------------|:------------------|
| `YEAR`       | The year when the outage occurred| 
| `MONTH` | The month when the outage occurred |
| `U.S._STATE` | State the outage occured in| 
| `OUTAGE.START.DATE`| Day of the year when the outage started |
| `'OUTAGE.START.TIME'`| Time of the day when the outage started |
| `RESTORATION.START.DATE`| Day of the year when energy was restored for outage|
| `'RESTORATION.START.TIME'`| Time of the day when energy was restored for outage|
| `CLMATE.CATEGORY`| Climate episode during outage (Warm/Normal/Cold) |
| `OUTAGE.DURATION`| Duration of outage (minutes) |
| `POPULATION`| Duration of outage (minutes) |
| `DEMAND.LOSS.MW`|  Amount of peak demand lost during an outage event (Megawatt) |
| `CUSTOMERS.AFFECTED`| Number of customers affected by a power outage event |
| `RES.SALES`| Electricity consumption in the residential sector (megawatt-hour)|
| `COM.SALES`| Electricity consumption in the commercial sector (megawatt-hour)|
| `IND.SALES`| Electricity consumption in the industrial sector (megawatt-hour)|
| `TOTAL.SALES`| Total electricity consumption in the U.S. state (megawatt-hour)|
| `UTIL.CONTRI`| % of Utility industry׳s contribution to the total GSP in the State|
| `NERC.REGION`| North American Electric Reliability Corporation (NERC) regions involved in the outage event|
| `CAUSE.CATEGORY`| Event causing the power outage|


# Data Cleaning and Exploratory Data Analysis 

## Here we outline the steps taken to clean our dataset so it is effective for analysis 
1. We  start by dropping missing rows and correctly labeled column titles with their corresponding features.We are only keeping the columns  that we are  working with for analysis. `YEAR`, `MONTH`, `U.S._STATE`, `CLIMATE.REGION`, `CLIMATE.CATEGORY`, `OUTAGE.START`, `OUTAGE.RESTORATION`, `CAUSE.CATEGORY`, `OUTAGE.DURATION`, `DEMAND.LOSS.MW`, `CUSTOMERS.AFFECTED`, `RES.SALES`, `COM.SALES`, `IND.SALES`, `TOTAL.SALES`, `POPULATION`]]
2. Then, we combined the `OUTAGE.START.DATE` and `OUTAGE.START.TIME` columns into a singular `OUTAGE.START` column that utilizes the Timestamp object. We followed the same for `OUTAGE.RESTORATION.DATE` and `OUTAGE.RESTORATION.TIME`, to get the comprehensive ending time for the outage (when the outage was restored). we then dropped the old columns since all the relevant timing was captured in `OUTAGE.START` and `OUTAGE.RESTORATION`
3. Next, we filled in missing values from the columns with NAN
Here is the first few rows of our cleaned dataframe. 

|    |   YEAR |   MONTH | U.S._STATE   | CLIMATE.REGION     | CLIMATE.CATEGORY   | OUTAGE.START        | OUTAGE.RESTORATION   | CAUSE.CATEGORY     |   OUTAGE.DURATION |   DEMAND.LOSS.MW |   CUSTOMERS.AFFECTED |   RES.SALES |   COM.SALES |   IND.SALES |   TOTAL.SALES |   POPULATION |
|---:|-------:|--------:|:-------------|:-------------------|:-------------------|:--------------------|:---------------------|:-------------------|------------------:|-----------------:|---------------------:|------------:|------------:|------------:|--------------:|-------------:|
|  0 |   2011 |       7 | Minnesota    | East North Central | normal             | 2011-07-01 17:00:00 | 2011-07-03 20:00:00  | severe weather     |              3060 |              nan |                70000 |     2332915 |     2114774 |     2113291 |       6562520 |      5348119 |
|  1 |   2014 |       5 | Minnesota    | East North Central | normal             | 2014-05-11 18:38:00 | 2014-05-11 18:39:00  | intentional attack |                 1 |              nan |                  nan |     1586986 |     1807756 |     1887927 |       5284231 |      5457125 |
|  2 |   2010 |      10 | Minnesota    | East North Central | cold               | 2010-10-26 20:00:00 | 2010-10-28 22:00:00  | severe weather     |              3000 |              nan |                70000 |     1467293 |     1801683 |     1951295 |       5222116 |      5310903 |
|  3 |   2012 |       6 | Minnesota    | East North Central | normal             | 2012-06-19 04:30:00 | 2012-06-20 23:00:00  | severe weather     |              2550 |              nan |                68200 |     1851519 |     1941174 |     1993026 |       5787064 |      5380443 |
|  4 |   2015 |       7 | Minnesota    | East North Central | warm               | 2015-07-18 02:00:00 | 2015-07-19 07:00:00  | severe weather     |              1740 |              250 |               250000 |     2028875 |     2161612 |     1777937 |       5970339 |      5489594 |

## Univariate Analysis 
We will begin by visualizing power outages by single variables.

#### Here we analyze the distribution of climate categories
It was important for us to first recognize the distributions of climate categories in a pie chart as it shows us what type of climate the majority of power outages occur in.
<iframe
  src="assets/univariate-plot-1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

#### Here we analyze the frequency distribution of outages per month 
The bar graph illusrates a potential predictor for people affected bt power outages, such as month of year, since we notice there is a high frequency of outages in summer months.
<iframe
  src="assets/univariate-plot-2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


#### Bivariate Analysis 
Sam explain this 
<iframe
  src="assets/bivariate-plot-1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
explain some more sam 
<iframe
  src="assets/bivariate-plot-2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
explain this too sam 

#### Grouping and Aggregates 
sam why did you choose to do the pivot table this way 

| CAUSE.CATEGORY                |        2000-2003 |       2005-2008 |        2009-2012 |        2013-2016 |
|:------------------------------|-----------------:|----------------:|-----------------:|-----------------:|
| equipment failure             | 897928           |     1568480 | 329604           | 262055           |
| fuel supply emergency         |      0           |     0           |      0           |      1           |
| intentional attack            |      0           |     0           | 133234           | 223081           |
| islanding                     |      0           | 49646           |  63164           |  96939           |
| public appeal                 |  55800           | 16000           |  88194           |      0           |
| severe weather                |      25976868 |     44932491 |      43023494 |      21275280 |
| system operability disruption |      11209646 |     3075918 |      2426558 | 806358           |

what does this table show us sam?

# Assessment of Missingness
## NMAR Analysis 

The `YEAR`column is likely to be NMAR because the occurrence of an outage in a particular year is typically independent of other features within the dataset. Each outage event should have an associated year, and the missingness of a `YEAR` value would generally not be influenced by the outage's characteristics, but rather the way the data was reported and collected, such as certain companies not reporting data into a source. Therefore, the missingness in the `YEAR`n column would typically depend on the value of the data itself. Additional data that we could collect to determine if the missingness is MAR is collecting information on the documentation practices of power outages over the years, including any regulatory changes in reporting requirements or practices that might have occurred. With this, we could analyze if there is an association between a change in reporting practices, with the missingness of the year values, making it MAR.

## Missingness Dependency 

Looking at the dataset, there are many columns that have missingness that can be assessed, but we focused specifically on the `DEMAND.LOSS.MW`, because we wanted to analyze whether power was supplied efficiently when experiencing an outage. We will test against the missingness using columns `CAUSE.CATEGORY` and `MONTH`. 

### Cause Category
Firstly, we evaluated the distribution of `CAUSE.CATEGORY` when `DEMAND.LOSS.MW `is missing vs not missing.

**Null Hypothesis**: The distribution of CAUSE.CATEGORY is the same when DEAMND.LOSS.MW is missing vs not missing.
**Alternate Hypothesis**: The distribution of CAUSE.CATEGORY is different when DEMAND.LOSS.MW is missing vs not missing.
<iframe
  src="assets/cause-bar-plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/cause-dist-chart.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

We observed a total variation distance (TVD) of 0.179,  with a a p value of 0.0 (alpha 0.01). At this value, we reject the null hypothesis in favor of the alternative, establishing that the distribution of CAUSE.CATEGORY.  CAUSE.CATEGORY  is significantly different when DEMAND.LOSS.MW is or is not missing, indicating that the missingness of DEMAND.LOSS.MW is dependent on CAUSE.CATEGORY.

### Month
Secondly, we evaluated the distribution of `MONTH` when `DEMAND.LOSS.MW` is missing vs not missing.

**Null Hypothesis**: The distribution of `MONTH` is the same when `DEMAND.LOSS.MW ` is missing vs not missing.
**Alternate Hypothesis**: The distribution of `MONTH` is different when `DEMAND.LOSS.MW ` is missing vs not missing.

<iframe
  src="assets/month-bar-plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/month-dist-chart.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

We analyze an observed Total Variation Distance (TVD) of 0.103, with a p-value of 0.026 (alpha 0.01).  At this value, we fail to reject the null hypothesis in favor of the alternative. The distribution of MONTH is not significantly different when `DEMAND.LOSS.MW`  is missing or not missing, indicating that the missingness of `DEMAND.LOSS.MW` is not dependent on Month.
