### Starbucks Capstone Project

#### Description

The project was introduced by Richard Sharp, Data Scientist at Starbucks. This project contains simulated data to mimic users of the Starbucks app. The data models Starbucks sending out offers (Buy One Get One/BOGO, Discounts off a purchase, and Informational offers. The goal of the project is to create and demonstrate a framework that can be used to discover which offers are the best for each user. We will accomplish this by creating user segments. Since this project was not conducted as a random experiment, no causality can be concluded.

#### Data Source:

Data for this project was provided by Udacity at the following URL
https://classroom.udacity.com/nanodegrees/nd025/parts/84260e1f-2926-4127-895f-cc4432b05059/modules/78dd932d-67a7-4039-9907-f8e6211e4590/lessons/d6285247-6bc0-4783-b118-6f41981b9469/concepts/59623bdf-9fdf-4b34-a5f8-c56dc75fc512

### Problem Statement

As was mentioned in the previous paragraph, this project seeks to identify which offers are effective for what people. This will be accomplished using data manipulation and feature engineering. In addition, we will seek to understand which features are more important in determining if an offer is effective, and finally, seeing if we can predict which offer types are effective.
In exploring the data, we will also seek to answer the following questions:<br>
1)	How does the total amount spent vary by gender?<br>
2)	Is there a difference in the average spend by membership tenure?<br><br>
3)	How does income differ by membership tenure?<br>
4)	Which media was used for each offer?<br>
5)	Which offers had the most transactions?<br>
6)	What is the average income by age segment?<br>
7)	What does income look like for users by age and gender? <br>
8)	Which offers are most successful overall?<br>
9)	Do females or males appear more likely to respond to offers?<br> 
10)	Which offers are more effective for each gender?<br>
11)	How does the total number of transactions for effective offers compare by gender?<br>
12)	What types of effective offer does each gender seem to prefer?<br>
13)	What is the average price per transaction for each offer group (1,2,3,4)?<br>
14)	What are the total transactions per group?<br>
15)	What customers should not receive offers?<br>

As this data was not part of a randomized experiment, findings are not assumed to have causality.

#### Libraries used in this project:

Python 3<br>
pandas <br>
numpy<br>
math<br>
json<br>
matplotlib, pyplot<br>
DecisionTreeClassifier<br>
RandomForestClassifier<br>
train_test_split<br>
StandardScaler<br>
Pipeline<br>
accuracy_score<br>
confusion_matrix<br>
f1_score<br>
cross_val_score<br>
GridSearchCV<br>
metrics<br>
classification_report<br>
warnings<br>
seaborn<br>

### Dataset Overview:

The simulated data used in this analysis is contained in three files:<br>

•	portfolio.json - containing offer ids and meta data about each offer (duration, type, etc.)<br>
•	profile.json - demographic data for each customer<br>
•	transcript.json - records for transactions, offers received, offers viewed, and offers completed<br>

Here is the schema and explanation of each variable in the files:

#### portfolio.json
•	id (string) - offer id<br>
•	offer_type (string) - type of offer ie BOGO, discount, informational<br>
•	difficulty (int) - minimum required spend to complete an offer<br>
•	reward (int) - reward given for completing an offer<br>
•	duration (int) - time for offer to be open, in days<br>
•	channels (list of strings)

#### profile.json
•	age (int) - age of the customer<br>
•	became_member_on (int) - date when customer created an app account<br>
•	gender (str) - gender of the customer (note some entries contain 'O' for other rather than M or F)<br>
•	id (str) - customer id<br>
•	income (float) - customer's income<br>

#### transcript.json
•	event (str) - record description (ie transaction, offer received, offer viewed, etc.)<br>
•	person (str) - customer id<br>
•	time (int) - time in hours since start of test. The data begins at time t=0<br>
•	value - (dict of strings) - either an offer id or transaction amount depending on the record<br>

Using a variety of data wrangling techniques, I evaluated the file, discovering a number of opportunities to improve the quality and tidyness of the data. The following issues were found with the datasets:

### Summary of dataframe issues

#### Portfolio
•	channels have multiple items. We should break this into separate columns.<br>
•	Separate the offer types into individual columns<br>
•	Consider changing the portfolio ID so it is between 1 and 10 to make for better visibility<br>
•	Rename id to offer_number as it can be confused with the id in the profile dataframe<br>
•	Convert the time field from days to hours to match transcript

#### Profile
•	Some participants appear to have an excessive age of 118. Investigate further.<br>
•	became_member_on should be converted to datetime<br>
•	Some gender are showing as None<br>
•	We should consider simplifying id to be a number starting at 1 and renaming id to user_id for clarity<br>
•	Income has some NaNs. Will need to consider how to treat these NaNs.<br>
•	became_member_on should be converted to datetime

#### Transcript
•	Need to clean the value column of the "{'offer id': " and "}"<br>
•	Some rows in the value column contain a combination of the offer id and reward amount. These will need to be separated and cleaned<br>
•	The value field also contains some amounts (spend). These will also need to be cleaned and placed into their own separate column.

### Main features of the dataset driving my interest:

I have a rich history as a Product Manager.  I am very interested in using data to drive Product Management decisions.  This dataset gives me a chance to fully demonstrate how data is collected, cleaned, analyzed and used to predict the success of promotions.  Segmentation details will allow Product Mangers to make better decisions to target their user base and grow app participation.

### Summary of Findings:

The following aspects were found interesting in the data:<br>
•	Looking at user profile data, the median income is $64,000. <br>
•	The largest reported income in the group was 120,000 and it was reported by user 17000.<br>
•	Females seem to report a slightly higher mean income than males.  <br>
•	While the effective offer group has slightly more male users, the female users are spending more. <br> 
•	Customers in the 1-3 year tenure group tended to purchase more, followed by the 3-5 year group.<br>
•	There appear to be slight differences in median income. Users in the 1-3 year range have 62,000 dollars in median annual income, while users in the 3-5 year range have 59,000 dollars in median annual income.<br>
•	Offers 6, 7 and 9 had the largest number of media types, reaching the largest number of users. Offers 3, 4, 5, 8 and 10 had fewer media types than the other offers. <br> 
•	Offer number 7 had the largest number of transactions, followed by 9 and 1. <br> 
•	There appear to be a slightly larger group of males reached by the effective offers.<br>
•	Offers 1 and 2 are slightly more effective for female when compared to simulated male users.<br>
•	Offers 4, 6, 7, 9 and 10 had at least a 6% difference in effectiveness compared to the simulated female users.<br>
•	While female users spend more than males, the males have a larger number of transactions.<br>
•	For females, discount and gender are almost equally prefered, while males clearly prefer discount. Users with undefined gender clearly preferred discount to BOGO.<br>
•	In all cases, informational promos were least preferred.<br>
•	The data seems to confirm that users assigned to group 1 (effective offers) spend more than those in group 3 (customers who purchase regardless of offer). While this would seem to indicate it makes sense to provide these promotions, financial analysis would need to be conducted to ensure there is a cost benefit.<br>
•	We were successful in creating a machine learning model to identify which offers are effective for users. Using a combination of user, transaction, offer and engineered feature data, we were able to achieve over 90% test accuracy.  We demonstrated that a machine learning model can be created to predict if an offer will be effective.  Membership Tenure, Age, Income, and amount spent are the most important features.  

### Files in the Repository

•	starbucks_capstone_ntbk_v1 – The Jupyter notebook containing a detailed analysis and machine learning models.<br>
•	data <br>
|- portfolio.json # contains information regarding the offers<br>
|- profile.json # contains detail regarding individual users<br>
•	transcript.json # contains user transaction data <br>
•	transaction_master.csv # contains detailed transaction, user profile and offer/portfolio data including the group a user is assigned to based on offer completion.<br>
• Starbucks_Framework.html # Blog containing a detailed analysis of the data and predictive model

### Program Execution
The program can be executed by starting Python 3, loading the Jupyter notebook and choosing “Kernel: from the drop down menu and choosing “Restart and Run All”.
Caution:  The Pipeline and GridSearch code may take at least 8 hours or longer to run depending on your computer speed and available memory.


