# Cardiovascular Disease Prediction (Classification)


## Objective
The main objective of this project is to build a binary classifier model, which predicts whether a person is at a 10-year risk of future coronary heart disease (CHD) on the basis medical history and other information.

## Dataset used
 The dataset provides the patient's information about following features.



```
- Sex : male or female ("M" or "F") (Nominal)
- Age : Age of the patient 
- Education : Education level of the patient ( 1: lowest to 4 : highest) (ordinal)
- is_smoking : whether or not the patient is a current smoker ("YES" or  “No”) (Nominal)
- CigsPerDay : the number of cigarettes that the person smoked on average in one day.
- BPMeds : whether or not the patient was on blood pressure medication (0 or 1) (Nominal)
- prevalentstroke : whether or not the patient had previously had a stroke (0 or 1) (Nominal)
- prevalenthyp : whether or not the patient was hypertensive (0 or 1) (Nominal)
- Diabetes : whether or not the patient had diabetes (0 or 1) (Nominal)
- TotChol : total cholesterol level (Continuous)
- sysBP : systolic blood pressure (Continuous)
- diaBP : diastolic blood pressure (Continuous)
- BMI : Body Mass Index (Continuous)
- HeartRate : heart rate (Continuous)
- Glucose : glucose level (Continuous)
- tenyearchd : 10-year risk of coronary heart disease CHD (binary: “1”, means “Yes”, “0” means “No”) - DEPENDENT VARIABLE


```

- Total number of rows in data : 3390
- Total number of columns : 17
## Data Cleaning and Feature Engineering

### (1) Removing Duplicate rows
- No duplicate rows were present in dataset.

### (2) Handling null values
- Null values were found in following columns

* `Education`, `BPMeds` - Categorical features
* `cigsPerDay`, `totChol`, `BMI`,`heartRate`,`glucose` - Numerical features

To remove null values I have used SimpleImputer using
- mode for categorical features
- median for numerical features

### (3) Feature encoding
- Used Label encoding to transform categorical features - `sex`, `is_smoking`.

### (4) Handling skewness
- Used square root transformation to reduce skewness of `cigsPerDay`.
- Used logarithmic transformation to reduce skewness of `totChol`,`sysBP`,`BMI`,`heartRate`,`glucose`.


### (5) Rescaling of features
- Used `StandaedScaler` for rescaling of features.This step scales data into a uniform format that would utilize the data in a better way while performing fitting and applying different algorithms to it. 

## Exploratory Data Analysis

Visualization of data were mainly performed using Matplotlib and Seaborn libraries and the following graph and plots had been used:
  - Bar Plot.
  - Histogram.
  - Scatter Plot.
  - Line Plot.
  - Heatmap.
  - Box Plot
  - Pair Plot
             


- Out of 3390 given patients records almost 500 patients had cardiovascular disease. Hence, the dataset found to be imbalanced.
- Out of 87 diabetic patient 35 patients had cardiovascular disease.
- Out of 100 patients on BP medications 34 had cardiovascular disease.
- Out of 22 hypertensive patients 10 had cardiovascular disease.
- With increasing age risk of cardiovascular disease found to be increasing.
- `diaBP` and `sysBP` found to be stongly correlated.
- `sysBP` found to be moderately correlated with `prevalenthyp`, i.e. prevalent hypertension.
- `glucose` level also found to be moderately correlated to whether `Diabetes`.
- Risk of cardiovascular disease found to be not strongly depending on eduacation level.
- Men are found to be at higher risk of cardiovascular disease.
- Smoking increases risk of cardiovascular disease.

### Feature Selection

Feature Selection is crucial step before model training as it improves the performance of model and also to reduce multicollinearity in dataset.


```

         Feature selection increases the predictive power of machine learning algorithms by selecting the most important variables 
         and eliminating redundant and irrelevant features. For seelcting features I have used `Chi- Square test` for categorical features and `corraltion heatmap` for          numerical features.         
         (a) Chi-Square test (for categorical features): 
                 (i)   Found p-value of `is_smoking` very high. Therfore dropped it.
                 
                 
          (b) Correlation heatmap (for numerical features):
          
                 (i) Dropped 'diaBP` due to high correlation with `sysBP`.   
                 
          Also `id` column is dropped as it is unqiue for each row and therefore does not provide any information in training model.
```

### Features for model building

Input features used for model building are as follows:


```
- Sex 
- Age
- Education
- CigsPerDay 
- BPMeds 
- prevalentstroke 
- prevalenthyp 
- Diabetes 
- TotChol 
- sysBP
- BMI 
- HeartRate 
- Glucose 

```

## Handling imbalanced dataset

```
Imbalanced dataset can make model highly inaccurate. Therefore handle imabalanced dataset we have used SMOTE boosting.

```


## Model Building


Since we have to predict whether person has a 10-year risk of future coronary heart disease (CHD) , so this is a binary classification problem. Based on the problem statement which is basically to predict whether person has a 10-year risk of future coronary heart disease (CHD) I decided to develop predictive models using following algorithms and have compared there performance.
```
- Logistic Regression
- SVM Classifier
- Random Forest Classifier
- Gradient Boosting Classifier
- KNN Classifier



Following necessary steps have been employed for better model performance.
                (i)   train test split for model evaluation.
                (ii)  Hyperparameter tuning for best learning parameters that developed a better model. Hyperparameter tuning was done with the help
                      of RandomizedSearchCV.
                (iii) Since the dataset is inbalanced, therefore default value of threshold(0.5) can result in inaccurate model. Therefore, I have tuned threshold                           value also to make models more accurate.
                      
                      
                  
```


### Evaluation metrics

To evaluate the models I have used `Recall`, `F1-score` and `roc_auc_score`.


## Conclusion

```
                 (i)   All models had lower recall score due to imbalanced data and using threshold = 0.5 (default)
                 (ii) Logistic regression was most accurate as compared to other models
                          Recall for test dataset         = 0.6773
                          roc- auc score for test dataset = 0.6803
                          f1- score                       = 0.3554
                 (ii) Using lower threshold value (< 0.4) improves recall significantly and f1-score also improves slighlty.
                         Recall for test dataset         = 0.78 
                         f1- score                       = 0.37 
           

```
## Challenges
```

                (i) Handling imbalanced data was a tedious task.
                (ii) Building models using small size dataset was difficult.
                

```
