# FEMA_disaster_funding
Project 4- Disaster Funding in the U.S. 

## Contributors

Nancy Frye
Barbara Kocurek
Katherine Okray
Bharti Sharma


## Description

This analysis focuses on FEMA data and the different funding types when faced with natural disasters. Data Model Implementation and Optimizations were completed to investigate the allocation of FEMA funding for public infrastructures such as roads and bridges, water control facilities, public buildings, etc. The allocation of public funding is key to re-building community infrastructure and recovery. 


## Questions/Wonderings

We focused on Other Needs Assistance (ONA) because this category is less well-known in FEMA categories. 

We examined whether there is a connection between different types of disaster funding allocated. 

We examined whether disaster funding differs based on types of disaster. 


## Analysis/Findings

Necessary dependencies were imported, and two FEMA CSV files were read. The first CSV file focuses on the types of funding given per disaster type. The second CSV focuses on information about each disaster type (i.e., When, Where, What?). Temporary SQL tables were created in order to merge the data. The tables were merged based on the Disaster Number. This new merged table included how much aid went into infrastructure, other types of aid, the year of the disaster, and the type of disaster. 

Cleaning and filtering were completed after we found that some disasters had negative amounts of aid. As a result, we focused only on disasters with support amounts of 0 or higher. After reading in the Pandas DataFrame, we replaced missing values for ONA. Total ONA never fell to zero funding, so we assumed any missing values would be replaced with zeros. 

We used Dummy coding to view the various types of disasters. From there, we conducted linear regressions to predict how much money went into infrastructure support. We found that ONA needs more funding than infrastructure support. Once about 4 million dollars was given to ONA, no support was given for infrastructure support, shown by our model intercept y = -4,614,407 + 7.95X. This model demonstrated an R-squared value of 0.32. 

We then looked to see if the type of disaster affects infrastructure support, one at a time. The first type, Severe Storms, showed they get less infrastructure support than disasters not in the category of Severe Storms. Hurricanes were reviewed next and showed a positive slope, meaning there was more support when the disaster type was a Hurricane versus when the disaster type is not a Hurricane. To dig deeper, we wanted to predict if support was given based on new information. A column was added indicating whether or not infrastructure support was given. Once this new column was added, we merged with the Dummy data for a new dataset. 

Variables for X and Y were selected as follows: 
X was for predicting variables (ONA, Year, Dummy code for type of disaster). 
Y was whether or not infrastructure support was given. 

A Logistic Regression was run and returned a low accuracy of 50%. We used a Random Oversampler to balance our data. The Dummy coded data, Year, and ONA were very different values, so we scaled the data using a Standard Scaler. The Logistic regression was rerun and returned a 43% classification accuracy. Using Neural Network Modeling helped to improve the fit of the model. ‘Relu’ and ‘Sigmoid’ activation functions were also utilized to improve fit. After training the model, the predictive power demonstrated a 71% classification accuracy. Another layer with three units was added, and the ‘tanh’ activation function was used. This resulted in the classification accuracy to increase to 83.7%. 


## Exploratory analysis

We wanted to see if we could predict the type of disaster based on the assistance given. Any disaster values under 1,000 counts were moved to the category of “other” to consolidate the results, leaving us with five types of disasters: Severe Storm, Hurricane, Flood, Severe Ice Storm, Snow Storm, and Other. We used a Random Forest classifier model to predict the types of disaster categories with 99% classification accuracy. The most important feature was how much infrastructure support was given. Specifically, Hurricanes had the most infrastructure support. This showed a seven times greater support than Earthquakes, the second category with the greatest support. 


## Limitations

https://www.fema.gov/api/open/v1/FemaWebDisasterSummaries.csv
The data set contains financial assistance values, including the number of approved applications and individual, public assistance, and hazard mitigation grant amounts. This raw, unedited data from FEMA's National Emergency Management Information System (NEMIS) is subject to a small percentage of human error. The financial information is derived from NEMIS, not FEMA's official financial systems. Due to differences in reporting periods, the status of obligations, and how business rules are applied, this financial information may differ slightly from official publications on public websites such as usaspending.gov; this dataset is not intended to be used for any official federal financial reporting. Also, annual inflation was not considered/adjusted.
