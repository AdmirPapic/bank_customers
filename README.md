# Bank Customer Segregation: Project Overview 
* Created a tool that segregates customers of one of India's banks in order to help organizations identify and understand each segment of their customers
* Cleaned the dataset and selected only relevant customer features
* Optimized, compared and utilized KMeans Clustering, Hierarchical clustering, and DBSCAN models using model performance metrics and numerous visualizations in order to obtain the best model 
* Conducted detailed data analysis for each segment of customers

## Resources 
**Python Version:** 3.11.5

**Packages:** pandas, numpy, scipy, scikit-learn, matplotlib, seaborn, geopy, folium  

**For Web Framework Requirements:**  ``pip install -r requirements.txt`` 

**Dataset:** https://www.kaggle.com/datasets/shivamb/bank-customer-segmentation

**Plotting bubble map of India:** https://python-graph-gallery.com/bubble-map/,

**Obtaining geographical coordinates:** https://www.tutorialspoint.com/how-to-get-the-longitude-and-latitude-of-a-city-using-python

## Dataset
The Bank Customer Segmentation consists of 1 Million+ transaction by over 800K customers for a bank in India. The data contains information such as - customer age (DOB), location, gender, account balance at the time of the transaction, transaction details, transaction amount, etc.

## Data Cleaning
Many changes have been made to the original dataset in order to prepare it for training actual machine learning models:
 
*	Rows with empty cells were removed
*	Converted dates of birth to a consistent and nicer datetime format
*	Calculated ages of customers based on their dates of birth
*	Concluded that CustomerID is not unique to a single customer
*	Assumed that two or more rows with the same date of birth, gender, location and account balance are actually transactions of the same customer (since CustomerID can no longer be used to differentiate them)
*	Selected only features which are relevant to a customer: gender, location, age and account balance
*	Dropped duplicate rows, ensuring that each row represents a single customer

  ## Exploratory Data Analysis
The mean, minimum, 25%, medium, 75%, and maximum for numeric features were examined. Histograms, scatter plots and barplots for a number of features were examined.
