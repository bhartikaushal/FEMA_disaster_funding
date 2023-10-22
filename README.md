# FEMA_disaster_funding
Project 4- Disaster Funding in the U.S. 

## Contributors

Nancy Frye
Barbara Kocurek
Katherine Okray
Bharti Sharma


## Description

This analysis focuses on FEMA data and the different funding types when faced with natural disasters. Data Model Implementation and Optimizations were completed to investigate the allocation of FEMA funding for public infrastructures such as roads and bridges, water control facilities, public buildings, etc. The allocation of public funding is vital to rebuilding community infrastructure and recovery. 


## Questions/Wonderings

We focused on Other Needs Assistance (ONA) because this category is less well-known in FEMA categories. 

We examined whether there is a connection between different types of disaster funding allocated. 

We examined whether disaster funding differs based on types of disaster. 


## Analysis/Findings

Necessary dependencies were imported, and two FEMA CSV files were read. The first CSV file focuses on the types of funding given per disaster type. The second CSV focuses on information about each disaster type (i.e., When, Where, What?). Temporary SQL tables were created to merge the data. The tables were merged based on the column' Disaster Number'. This new merged table included how much aid went into infrastructure, other types of aid, the year of the disaster, and the type of disaster. The Sql table was then converted to a pandas data frame.
The dataset had some 'amount of aid' values below zero; we dropped those values and included the aid values above zero. The missing values in the 'Other Needs Assistance' column were replaced with a zero. 
We used Linear Regression to predict the amount of funds allocated for infrastructure    (CatC2g) based on the amount allocated for Other Needs Assistance(ONA). We noticed the amount of funds for infrastructure are allocated only after a certain amount has been spent on Other Needs Assistance. It kicks in after about 4 million dollars have been spent on ONA, as shown by our model equation, i.e., y = -4,614,407 + 7.95x. This model demonstrated the R-squared value of 0.32. This shows a weak correlation between the two features.
Using Linear regression, we then looked to see if the type of disaster affects infrastructure support, one at a time. We found that the maximum funds for infrastructure aid are provided for Hurricanes. Severe storms get less infrastructure aid.
 To dig deeper, we wanted to predict if 'Infrastructure Aid' was given based on other features in the dataset, like the type of disaster, the year it took place, and the funds allocated for ONA. A column was added indicating whether or not infrastructure support was given. Once this new column was added, we used dummy coding for the types of disasters and merged dummy codes with the dataset. Variables for X and Y were selected as follows: X was for predicting variables (ONA, Year, Dummy code for type of disaster). Y was whether or not infrastructure support was given.
A Logistic Regression was run and returned a low accuracy of 50%. We used a Random Oversampler to balance our data. The Dummy coded data, Year, and ONA were very different values, so we scaled the data using a Standard Scaler. That did not improve the accuracy of our model. We then used Neural Network Modeling to improve the fit of the model. We used Tensorflow(Keras) with 'relu' as the activation function. It did improve the accuracy of the model; it went up to 71%. We tried to optimize the model by adding a layer, increasing the number of units, and using a different activation function (tanh). It improved the model, and the accuracy of the model increased to 83.7.


We then tried to predict the type of disaster based on other features in our dataset. Any disaster values under 1,000 counts were moved to the category of "other" to consolidate the results, leaving us with five types of disasters: Severe Storm, Hurricane, Flood, Severe Ice Storm, Snow Storm, and Other. We used a Random Forest classifier model to predict the types of disaster categories with 99% classification accuracy. The most important feature was how much infrastructure support was given. Specifically, Hurricanes had the most infrastructure support. This showed a seven times greater support than Earthquakes, the second category with the maximum support.



## Limitations

https://www.fema.gov/api/open/v1/FemaWebDisasterSummaries.csv
The data set contains financial assistance values, including the number of approved applications and individual, public assistance, and hazard mitigation grant amounts. This raw, unedited data from FEMA's National Emergency Management Information System (NEMIS) is subject to a small percentage of human error. The financial information is derived from NEMIS, not FEMA's official economic systems. Due to differences in reporting periods, the status of obligations, and how business rules are applied, this financial information may differ slightly from official publications on public websites such as usaspending.gov; this dataset is not intended to be used for any official federal financial reporting. Also, annual inflation was not considered/adjusted.
