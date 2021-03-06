# lending_club
## Repo for Data Science Classification

## Goal
Given historical data on loans given out with information on whether
or not the borrower defaulted (charge-off), I am building a model that
can predict wether or nor a borrower will pay back their loan.

## Code and Resources Used
### Python
3.7.7
### Packages:
tensorflow 2.0 (with keras), numpy, pandas, sklearn, matplotlib, seaborn, 


## Data
I am using LendingClub DataSet obtained from Kaggle:
https://www.kaggle.com/wordsforthewise/lending-club
.

There are 27 fields in the dataset. For all the fields,
and their description, please look at the notebook.
Some of the fields are:
* loan_amnt
* term
* int_rate
* installment
* grade
* sub_grade
* issue_d
* title
* addr_st
* emp_title
* emp_length
* purpose
* mort_acc
* total_acc
* home_ownership
* verification_status
* application_type
* initial_list_status
* loan_status: is the column containing the label.

## Data Cleaning/Feature Engineering
I made the following changes:

* Created loan_repaid column which now has the label.
* Dropped emp_title as there were 173105 unique titles
* Drop emp_length as it did not impact the label much
* Dropped title column as it is containted in purpose column
* Imputed total_acc for missing values of mort_acc
* Dropped rows with NAN in revol_util and pub_rec_bankrputcies
* Dropped grade because it is contained in sub_grade
* Changed term into categorical column
* Changed sub_grade into categorical column
* Changed verification_status,
application_type,initial_list_status,purpose into categorical columns
* Changed home_ownership into categorical column
* Created zip_code from address
* Dropped address
* Dropped column issue_d as this is data leakage. 
* Created column having date from earliest_cr_line

## EDA
I looked at the distributions the value counts for the various
categorical variables. Below are a few highlights.

![alt text](https://github.com/sanrioyt/lending_club/blob/master/correlation.png "Check")
![alt text](https://github.com/sanrioyt/lending_club/blob/master/sub_grade.png "Correlation")
![alt text](https://github.com/sanrioyt/lending_club/blob/master/sub_grade2.png "Correlation")

## Model Building

I tried six different models and evaluated them using different metrics. 
I used classification_report and confusion_matrix for all of them,
and wanted to diminish val_loss for all the deep learning models.

I tried six different models:
* **Deep Learning Model model1**: No dropout, l2 reg=0.01 on bias and weights, and 
l2_reg=1e-5 for outouts
* **Deep Lerning Model model2**: Dropout=50%, l2 reg=0.01 on bias and weights and 
l2_reg=1e-5 for outputs
* **Deep Lerning Model model3**: Dropout=25%, l2 reg=0.001 on bias and weights and 
l2_reg=0.001 for outputs
* **Deep Lerning Model model4**: Dropout=25%, No regularization
* **RandomForestClassifier**
* **LogisitcRegression**

## Model Performance

Model4 (Deep learning model) with 25% dropout and no regularization, and 4 
hidden layers performed the best (For val_loss, classification report, and confusion_matrix).

