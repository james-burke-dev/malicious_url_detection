## Initial Notes 
- This project was completed as part of my Certificate of Data Analysis: Machine Learning form Univeristy College Dublin 
- To run this notebook you will need to place the train and test dataset from https://www.kaggle.com/datasets/pilarpieiro/tabular-dataset-ready-for-malicious-url-detection/data?select=train_dataset.csv in the data folder
- Please be aware the datasets contain over 8 million records which leads to a long runtime
- My results are contained within the results folder and the completed report is contained within the report folder


## Introduction 
Cybercriminals will use any means necessary to comprise individuals’ or organization’s networks
to collect sensitive information. Malicious URLs can be used to extract information such as login
information or credit card details. Some of the information collected can then be leveraged to
further comprise networks which can then cause further damage to an organization or individual.
The impact of this can vary from monitoring computer systems on the network to deploying
ransomware within the network using comprised login information.

Blacklisting services have been developed to help detect harmful websites. A blacklist is a
database containing a list of all URLs that are known to be malicious. However, the blacklist likely
needs to be manually maintained. Changes to one or more components of the URL string may
result in the URL not being part of the blacklist and thus many malicious sites are not blacklisted.
This can be due to the site being too new, never assessed or assessed incorrectly.

The goal of this project is to determine if an AI solution is deployed to recognize malicious URLs,
how well would it detect a malicious URL when trained on a dataset containing an equal amount of
malicious and benign URLs.

## Data 
The Malicious URL detection dataset we are using for this project comes from Kaggle, located
at: https://www.kaggle.com/datasets/pilarpieiro/tabular-dataset-ready-for-malicious-url-detection/data?select=train_dataset.csv

The dataset contains two .csv files, one train.csv (containing 6,728,848 rows) and one test.csv
(containing 1,682,213 rows). Both files have the same 60 columns with the key columns to highlight
at this stage being “url”, "label" and "source".

Our target is the "label" feature with a value of 0 indicating a benign URL and 1 indicating a
malicious URL. The “url” is the unprocessed URL that is to be classified. The "source" column is a
reference to where the URL was gathered from.

The rest of the 57 features break the URLs down into each of the URL features.
The first set of features are lexical features. These are the elements of the URL string itself. Lexical
features include metrics like the URL length, the number of letters, special characters or digits in
the URL. The second set of features are network, DNS and host features. These include the
subdomain length, information about the top-level domain or if the URL contains an IP address.

## Models 

Classification methods were chosen for our project as our problem is a binary classification
problem where our target variables are two discrete values 0 (benign) and 1 (malicious).

With this known we made the decision to initially test two algorithms for binary classification,
Logistic Regression and the K Nearest Neighbor (KNN) classifier. In our initial testing KNN had a
higher accuracy score of 0.85 in comparison to the Logistic Regression’s accuracy of 0.82. Based on the higher accuracy value, we chose KNN to conduct further hyperparameter
tuning.

For our hyperparameter tuning we used GridSearch to test two hyperparameters, the number of
neighbors and the method of distance calculation. This resulted in our best combination of from
number of neighbors (5,7,9 or 11) and the distance calculation methods ('minkowski', 'euclidean'
or 'manhattan'), being tied between {'metric': 'euclidean', 'n_neighbors': 11} and {'metric':
'minkowski', 'n_neighbors': 11} with a mean accuracy score of 0.8641895153. The results of the
GridSearch can be seen in the “KNN_cv_results.csv” file included with the code submission.

## Conclusion 

Domain knowledge plays a key part in understanding the dataset and in the selection of features to
train the model on. With better knowledge of URLs and the features included in this dataset, we
believe better feature selection could be done. The selected features could then lead to improved
model predictions.

To conduct a full tuning of hyperparameters a high level of compute and length of time is needed.
Combining the cross validation from grid search and the number of combinations available with
the hyperparameters leads to a large number of jobs. We believe that further improvements can be
made to the model by tuning the hyperparameters further.

Additional hyperparameters that could be investigated could include the ‘weight’ function which is
used in the prediction or the ‘leaf_size’ which could improve the time taken for the model to complete and the memory required during its runtime.

Overall, we feel that there are more improvements to be made to the model at this stage. For
potential next steps with the project, we feel improved feature selection, bagging and ensemble
methods would be best explored.
