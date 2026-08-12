# Predicting the Death of US Tourism
DATASCI 207: Applied Machine Learning | Summer 2026 Section 2 | Final Project

Abigail Kreutz (abigailkreutz@berkeley.edu), Peter Huang (huangpeter@berkeley.edu), Hope Tadsen (hope_tadsen@berkeley.edu)

## Overview
This project investigates the ability to use machine learning to predict the number of monthly tourists visiting the United States based on socio-political and economic indicators. Our target label was the number of I-94 visas granted for tourists traveling to the U.S. To accomplish this, datasets showing monthly U.S. I-94 border crossings, GDP, political party alignment and armed conflict count by type were chosen for feature engineering.

Each group member's folder contains their respective EDA and data cleaning. The datasets were divided as such:
- Hope_EDA: Tourism inbound totals and GDP feature data
- Abby_EDA: Armed Conflict and Political Unrest (ACLED) feature data
- Peter_EDA: I-94 arrivals target label data and political party control feature data

Model_testing is our primary notebook used to conduct baseline analysis and where we conducted our first series of baseline modeling and feature engineering. Additional_Modeling is where the majority of the refinements to our modeling, including a separate experiment on ACLED was conducted.

## 📄 Full Report
You can view the full PDF report [here](Predicting%20The%20Death%20of%20US%20Tourism_Final%20Report.pdf).
  
## Updates:
### 03 AUG 2026: 
Final ACLED experimentation results and additional RandomForest and XGBoost modeling conducted in Additional_Modeling.

### 30 JUL 2026:
Model_Testing section has been updated to include RandomForest and XGBoost Modeling Results.

New notebook created called "Additional_Modeling". This was created to conduct additional experiments due to the unique nature of the ACLED dataset. Because ACLED
only accounts events from 2020 onward, additional models were created to attempt to isolate the effects of ACLED on I-94 arrivals only from 2020-2026.

### 19 JUL 2026:
Model_Testing notebook created. Two baseline models created and ran (average-predictor and linear regression)
Edited all three EDA notebooks to include creation of a cleaned feature/label .csv file that could be used in Model_Testing
New .csv files include: 
- label_arrivals_cleaned.csv 
- features_gdp_cleaned.csv 
- features_inbound_cleaned.csv 
- features_party_cleaned.csv 
- features_acled_cleaned.csv

###  28 JUN 2026:
Project Milestone: EDA completed by all group members for label (I-94 arrival data) and features. Each individual notebook and dataset was saved in separate folders
