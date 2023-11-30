# Project 4- Traffic Violations
------------
## Project Description

### Goal
Use EDA, machine learning, and visualization to analyze a dataset of traffic violations from Maryland from the years 2012 to 2023. 

------------
## Credits
ChatGPT was used for some portions for researching approaches to tasks. The data used was from https://data.montgomerycountymd.gov/.

------------
## Softwares Used
### Libraries
Pathlib
Scikit Learn
   ensemble.RandomForestClassifier
   linear_model.LogisticRegression
   model_selection.train_test_split
   metrics.confusion_matrix, accuracy_score, classification_report
Pandas
matplotlib

### Language
Python
SQL

### Software
VSCode
GitLens

------------
## Exploratory Data Analysis
-  Read the csv into a dataframe.
-  Dropped columns that were deemed to be represented by other columns or columns that were not valuable.
-  Dropped safety related violation types so that only violation types of warning and citation are the only
   rows left.
-  'Violation Type' is the target feature.
-  Dropped rows with invalid years.
-  Removed data that had the latitude and longitude set as zero.
-  Converted the 'Date of Stop' and 'Time of Stop' features to Year of Stop, Month of Stop, and Hour of Stop.
-  Dropped rows with a null description.
-  Used Regex to replace descriptions with specific key words to make the descriptions more uniform for
   machine learning modelling.
   -  Examples of some descriptions that were standardardized contain some or all of the words or phrases:
      -  Speeding: Exceeding Speed Limit, Speed, and Speeding
      -  Failure to Yield: Fail Yield and Failure Yield
      -  Learner Permit
      -  Improper Equipment: Lamp, Headlight, Required Minimum Equipment, and Inoperative
      -  DUI: Influence Alcohol and Impaired Alcohol
-  25 groups of descriptions were classified using regex to reduce the number of unique descriptions to 
   around 5000 descriptions which were then binned to make descriptions with less than 10,000 occurances be classified as 'Other' leaving the top 25 descriptions.
-  The license plate state feature was categorized into in-state (MD) and out of state (all others).
-  The Make feature contained many errors. The Make values were manually corrected through makes that had
   10 or more values in the dataset. The makes with 9 or less values were classified as 'Other'.
   -  If the make value did not have a clear correction, the value was set to unknown.
-  The Date of Stop, Driver State, State and Time of Stop features were dropped from the dataframe because the
   values contained in these columns was represented in other, more meaningful, columns.
-  The colors of cars were classified into neutral colors and colorful colors.
-  The resulting dataframe was written to a .csv file called Traffic_Violations_Processed to be used for 
   machine learning modelling.

## Machine Learning Modelling
-  The Traffic_Violations_Processed.csv was read into a dataframe.
-  The dataframe was limited to the columns 'Description', 'Accident', 'Alcohol', 'Search Outcome', 'Violation
   Type', and 'License Plate State Category'.
-  The rows with null values had the null value replaced with the word 'None'.
-  All of the remaining columns were one hot encoded with pd.get_dummies.

### Example of One Hot Encoded Features
![Alt text](image.png)

-  The features were separated from the target feature and assigned the variable X.
-  The target feature, 'Violation Type', was assigned the variable y.
-  The features and target were split into test data and train data with train_test_split.
-  A random forest model was instatiated, the training data was fit to the model, the model was used to predict
   the test data, a confusion matrix was calculated and the results of the confusion matrix were displayed.

### Random Forest Confusion Matrix
   ![Alt text](image-1.png)

-  A logistic regression model was instantiated with the solver 'sag', 200 max iterations, and random state of 1.
-  The training data was fitted with the logistic regression model, predictions were made with the logistic
   regression model on the test data, a confusion matrix was calculated and the results of the confusion matrix were displayed.

### Logistic Regression Confusion Matrix
![Alt text](image-2.png)



## Part 2: Updating the Database
- Updated the database with a new restaurant, Penang Flavours, with the information provided.
- Queried the BusinessType for Rastaurant/Cafe/Canteen to find the BusinessTypeID since the new entry did not contain the BusinessTypeID.
- Updated the Penang Flavours entry with the correct BusinessTypeID.
- Removed all of the establishments in the Dover Local Authority.
- Converted the latitude and longitude from string type to float type entries.
- Converted the RatingValue from string type to integer type.
    - This included setting all none numeric ratings to Null.

### Exploratory Analysis
- Answered the following questions:
  1. Which establishments have a hygiene score equal to 20? The answer is 41.
     This involved using count_documents with a query to find the establishments that meet the criteria, pretty printing the first result to verify that the query       executed correctly, and converting the results to a dataframe with Pandas.
  2. Which establishments in London have a RatingValue greater than or equal to 4? The answer is 33.
     This involved querying the establishments in london with a RatingValue of 4 or greater (using regex to find entries that included London), using     
     count_documents to find the number of documents, pretty printing the first result to verify the data was queried correctly, and converting the results to a   
     dataframe with Pandas.
  3. What are the top 5 establishments with a RatingValue of 5, sorted by lowest hygiene score (which corresponds with the best hygiene), nearest the the new            restaurant, Penang Flavours? see image below
     ![image](https://github.com/SamanthaMcKay/NoSQL-Challenge/assets/132176159/30d5ad9e-2f9b-4d22-8c79-977e481e0857)
    This involved retrieving the latitude and longitude of Penang Flavours, calculating the minimum and maximum latitudes and longitudes, sorting by hygiene score       in ascending order, limiting the query to the first five, and converting the results to a dataframe.
  4. How many establishments in each Local Authority area have a hygiene score of 0, sorted from highest to lowest count with the top ten local authority areas           printed out? See below image

     ![image](https://github.com/SamanthaMcKay/NoSQL-Challenge/assets/132176159/e480da9a-3723-49e9-8140-b296b0ced81f)

     ![image](https://github.com/SamanthaMcKay/NoSQL-Challenge/assets/132176159/3423a6d9-16dd-4ded-9602-da3151503ffb)

     This involved using an aggregation pipeline to find establishments with a hygiene score of 0, group by the LocalAuthorityName, count the number of entries for     each local authority, sort highest to lowest for the number of establishments in each local authority, pretty printing the first 10 results, and converting the     results to a dataframe.

## Conclusion
I learned much about Pymongo and PrettyPrint. I struggled with the aggregation pipeline in particular. I enjoyed diving deeper into noSQL databases and getting a refresher on SQL querying and the different flavours that SQL comes in. PyMongo is a powerful tool for querying. 
# Project_4