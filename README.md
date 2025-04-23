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
