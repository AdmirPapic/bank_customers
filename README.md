# Bank Customer Segregation: Project Overview 
* Segregated customers of one of India's banks in order to help similar organizations identify and understand each segment of their customers
* Cleaned the dataset and selected only relevant customer features
* Optimized, compared and utilized KMeans Clustering, Hierarchical Clustering, and DBSCAN models using model performance metrics and numerous visualizations in order to obtain the best model 
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
The mean, minimum, 25%, medium, 75%, and maximum for numeric features were examined. The following histograms, scatter plots and bar plots for different features were created and examined. A bubble map displaying the places with the most customers was created. The visualizations clearly show distributions for each of the relevant customer features.

![alt text](https://github.com/AdmirPapic/bank_customers/blob/master/images/base_age_hist.png "Age Distribution")

![alt text](https://github.com/AdmirPapic/bank_customers/blob/master/images/base_gender_bar.png "Gender Distribution")

![alt text](https://github.com/AdmirPapic/bank_customers/blob/master/images/base_scatter.png "Account Balance vs Age scatter plot")

![alt text](https://github.com/AdmirPapic/bank_customers/blob/master/images/india_bubble_map.png "Customer Locations")

## Model Building
Three different types of models were built and their performance was compared.
Feature distributions for each customer segment were examined.

* **K Means Clustering** – The optimal number of clusters was determined using the elbow method and it was concluded to be K = 3, as inertia drops off more slowly after that point.

![alt text](https://github.com/AdmirPapic/bank_customers/blob/master/images/inertia.png "Inertia vs K")

While the first two clusters show a similiar proportion between males and females, the third and the smallest one (Class 2) was dominated by males.

![alt text](https://github.com/AdmirPapic/bank_customers/blob/master/images/kmeans_gender.png "KMeans Gender Distribution")

The Account Balance vs Age scatter plot shows a clearer distinction between the three clusters.

![alt text](https://github.com/AdmirPapic/bank_customers/blob/master/images/kmeans_scatter.png "KMeans Clusters")

* **DBSCAN** – Multiple DBSCAN models with different epsilon (maximum distance between neighbors) hyperparameters were trained. However, only one of them organized clusters in a way in which each cluster would contain more than 10 members, resulting in the following scatter plot for the two clusters and customers which are labeled as noise.

![alt text](https://github.com/AdmirPapic/bank_customers/blob/master/images/dbscan_scatter.png "DBSCAN Clusters")

* **Hierarchical Clustering** – A Hierarchical Agglomerative Clustering model was trained for three clusters with ward linkage. The Hierarchical Clustering Dendogram was plotted.

![alt text](https://github.com/AdmirPapic/bank_customers/blob/master/images/hier_dendo.png "Dendogram")

The following scatter plot and bar plot show feature distributions for the three clusters.

![alt text](https://github.com/AdmirPapic/bank_customers/blob/master/images/hier_scatter.png "Hierarchical Clusters")

![alt text](https://github.com/AdmirPapic/bank_customers/blob/master/images/hier_gender.png "Hierarchical Gender Distribution")

## Model performance
While KMeans Clustering and Hierarchical Clustering result in similar clusters, DBSCAN falls short of recognizing the middle-aged, wealthy, and mostly male group as a cluster, and instead labels it simply as noise. This was to be expected, since DBSCAN usually performs poorly when there are huge differences between the densities of the clusters. 
*	**KMeans Clustering** provides the clearest separations between the three clusters and much interpretability.
*	**DBSCAN** does not recognize clusters which have a much lower density. The algorithm also demanded downsampling of the dataset due to memory shortages.
*	**Hierarchical Clustering** provides high interpretability (due to the dendogram). However, the vast majority of customers is segregated into a single cluster, the two largest clusters are not clearly separated, and the algorithm also demanded downsampling due to computational issues.

