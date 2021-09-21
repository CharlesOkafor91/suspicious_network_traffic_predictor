# suspicious_network_traffic_predictor

Peer-graded Assignment: Course Project
Supervised Machine Learning: Classification

Main objective: For this project, I will be working on using several classification and ensemble models to classify anomalies detected in a network system  using the kaggle competition dataset here. The purpose will be that of model interpretability - analysing and providing insight into the relationship between the inputs and the respective classes. That is to answer questions as to why the independent features predict the dependent attribute.

Brief description of the data set: The dataset was extracted from the Coburg Intrusion Detection DataSet (CIDDS) of network activities that occurred between 14th and 16th of March 2017 on Kaggle. These days sophisticated systems are being built to encounter server attacks and suspicious content. CIDDS is a concept to create evaluation datasets for anomaly-based network intrusion detection systems.
The external server attack logs are the most interesting part. The dataset consists of 13 active columns including the target column - Class. Details of the column are as below:

![image](https://user-images.githubusercontent.com/26352709/134158026-1ca8bb14-cdb8-4372-bf19-0d5b89436599.png)

Brief summary of data exploration and Feature Engineering: First I renamed the columns to just one word so I can subsequently use it easily. Then I changed the Date_first_seen column to a datetime data type so I can extract the Day and Hour information which I feel was useful in predicting the attack class. Then I dropped the original column and some other empty columns. Also, I modified the Source and Destination IP to the specific categories we want. Here is how I did those:

![image](https://user-images.githubusercontent.com/26352709/134158201-2801ddab-d0f1-4bb0-8c65-eb16bb316968.png)

I also categorised the source and destination ports to 2 columns. First column is to categorise them into 3 source categories - System port, User port and Dynamic port, then the second column is to categorise them into their respective protocols. I then made the Bytes columns to be in the same measure - changed the megabytes to just bytes. Then lastly for the Flags column: Flags in network connection are used to indicate a particular state of connection or to provide some additional useful information like troubleshooting purposes or to handle a control of a particular connection. However whenever a certain flag is not set, a dot (.) is used to indicate that. Therefore we need to break down the flags column into its various flagpoints to help the model understand when a flag is seen and what type of flag. Using dataset.info() to check, I had no missing value in my dataset as all not null counts were complete. Finally I removed all rows where Duration is 0 seconds as it is seen as no event. I then used LabelEncoder and OneHotEncoder to encode my categorical dataset, StratefiedShuffleSplit to split the data so all categories will be well accounted for in train and test set and then StandardScaler to scale the dataset.

Summary of training at least three linear regression models: 
Logistic Regression - With and Without Regularization: For the logistic regression, we developed 3 models - one without regularization, the other with L1 regularization and last one with L2 regularization. Here is our metrics:
	![image](https://user-images.githubusercontent.com/26352709/134158390-f03ddda7-00fc-4a2f-af66-ceba9988fdcc.png)
	
Decision tree Classification: We developed 2 models for the decision classifier. First without any hyperparameter tuning and cross validation then we developed the second with hyperparameter tuning and cross validation:

Without tuning: Our node count was 159 and tree depth 16
![image](https://user-images.githubusercontent.com/26352709/134158519-51f7cc64-247e-494d-8afa-d6a31d5008f5.png)

With hyperparameter tuning and cross validation: Our node count was 159 and tree depth 13
	![image](https://user-images.githubusercontent.com/26352709/134158583-ca2edcaf-dc95-47c4-a725-44c26bbd4290.png)

	We can see with hyperparameter tuning, our model is less overfitted and more accurate
	

Recommended Regression: Based on the MSE and R2 score, I will be recommending using the Ridge regression with alpha 0.01 and with polynomial features

Summary Key Findings and Insights: The decision Tree Classifier performed better than logistic regression without overfitting when we carry out hyperparameter tuning and cross validation. I believe using more ensemble methods may perform better.


