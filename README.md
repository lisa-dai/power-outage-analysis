# power-outage-analysis

Power outages can be devastating—its effects can range from small inconveniences to detrimental problems like safety hazards, disrupted communications, and economic losses. Loss of heating or cooling systems can be dangerous, particularly for vulnerable populations like the elderly or those with underlying health conditions, while food spoiling can be devastating for the food-insecure. Outages can also affect critical services like mobile phone service, landlines, banks, and gas stations, affecting daily life. However, if energy companies can predict power outage severity in advance, could they theoretically better prepare, allocate resources, and therefore minimize harm?

## Step 1: Introduction

The dataset used in this analysis, Major Power Outage Risks in the U.S., was conducted by Purdue's Laboratory for Advancing Sustainable Critical Infrastructure (LASCI). The dataset comprises of 1,534 major power outages across the continental U.S. between 2000 and 2016. Each outage entry includes 55 variables detailing the geographical location, regional climate data, land-use characteristics, electricity consumption patterns, and economic indicators of the affected states.

The purpose of this analysis is to explore trends in the given variables and power outage severity, motivated by the following research question:

**What are the characteristics of major power outages with high severity?**

In order to measure the "severity" of a power outage, I will use the duration of the outage, a continuous quantitative variable.

The following are the columns that were used at some point during my analysis: 
* <code>CLIMATE.REGION</code>: U.S. Climate regions as specified by National Centers for Environmental Information (nine climatically consistent regions in continental U.S.A.)
* <code>PC.REALGSP.REL</code>: 	Relative per capita real GSP as compared to the total per capita real GDP of the U.S. (expressed as fraction of per capita State real GDP & per capita US real GDP)
* <code>MONTH</code>: The month when the outage event occurred
* <code>CAUSE.CATEGORY</code>: Categories of all the events causing the major power outages
* <code>U.S._STATE</code>: The state in the continental U.S. in which the outage event occured
* <code>POSTAL.CODE</code>: The postal code (state abbreviation) of the state in which the outage event occured
* <code>TOTAL.PRICE</code>: Average monthly electricity price in the U.S. state (cents/kilowatt-hour)
* <code>OUTAGE.DURATION</code>: Duration of outage events (in minutes)

## Step 2: Data Cleaning and Exploratory Data Analysis

### Data Cleaning
1. **Cleaning Excel File** <br>
The data was given as an Excel file rather than a CSV. I opened the data in Google Sheets and determined numerous rows and columns of the sheet that were blank or irrelevant for data analysis. This included the first five rows, which were blank outside of general descriptions of the data.
2. **Replacing Missing Values** <br>
In the columns <code>OUTAGE.START.DATE</code>, <code>OUTAGE.START.TIME</code>, <code>OUTAGE.RESTORATION.DATE</code>, and <code>OUTAGE.RESTORATION.TIME</code>, I replaced any zero values with np.nan, treating them as missing data. A value of zero in these fields is unlikely to represent an actual measurement and is more plausibly a placeholder indicating that the true value is unavailable.
3. **Dropping Rows with Missing Values** <br>
In columns <code>CLIMATE.REGION</code>, <code>PC.REALGSP.REL</code>, <code>MONTH</code>, <code>U.S._STATE</code> and <code>OUTAGE.DURATION</code>, I dropped all rows in which the data was not applicable, as it was important for my analysis that these column's values were present.
5. **Combining Date and Time Columns** <br>
The dataset provides the start date and time of each power outage through the columns <code>OUTAGE.START.DATE</code> and <code>OUTAGE.START.TIME</code>. For the purposes of my analysis, I combined these into a single pd.Timestamp column named <code>OUTAGE.START</code>. Similarly, I merged <code>OUTAGE.RESTORATION.DATE</code> and <code>OUTAGE.RESTORATION.TIME</code> into a new pd.Timestamp column called <code>OUTAGE.RESTORATION</code>.
6. **Adding <code>MONTH.NAME</code> Column** <br>
The dataset provides the month the outage event occured using numbers (i.e. 1 for January). For the purpose of readability, I created a new column named <code>MONTH.NAME</code> which converted these into the names of the months instead.
7. **Extracting Relevant Columns** <br>
Finally, I dropped the columns that will not be used during my investigation.

 <iframe
 src="assets/outages-head.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

 ### Univariate Analysis
I began by looking at the distributions of relevant columns and drawing plots in order to get a better understanding of the data. First, I plotted a bar graph showing the distribution of power outages by major cause:

<iframe
 src="assets/fig-cause.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

You can see that the most common cause by far is severe weather, though intentional attacks also comprise a significant number of outages. This tells me that variables related to weather will likely be a good predictor for power outage severity.

<iframe
 src="assets/fig-region.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

 The Northeast region has the most number of power outages by far. The variety in power outage distribution among different power outages tells me that there may be some pattern with climate and power outage severity.

 ### Bivariate Analysis

 To further my investigation, I need to find patterns between columns to identify possible associations.

 <iframe
 src="assets/fig-state.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

This plot reveals that Wisconsin has the highest average outage duration, with New York and West Virginia following closely behind. Notably, most states with higheroutage durations on average are in either the Midwest/Eastern region of the United States, with the Western states having much lower average durations.

 <iframe
 src="assets/month-duration.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

 September, October, January, August, and December trend towards longer outage durations. These months tend to be colder, suggesting again that weather may be correlated to power outage duration.