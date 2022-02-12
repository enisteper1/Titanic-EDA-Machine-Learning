# Titanic: EDA & Machine Learning (Top 3%)
The Titanic dataset is one of the basic datasets at Kaggle which purposes to predict survivors from Titanic disaster. Also, it has low data size, but gives high oppurtunity for feature engineering. At first, each feature will be handled one by one and then machine learning models will be trained and compared. At last, selected model with processed data will be submitted. Here is summary given of processing steps. You can check Titanic.ipynb, Titanic.html files or my Kaggle profile for the explanations with the codes. 

There are 3 sections at total which are:

* EDA & Feature Engineering
* Machine learning Model Selection
* Submission

## 1. EDA & Feature Engineering
## 2.1 Features
* **Sex Feature:** Most of these survivors are female, but men count approximately doubles count of women. From this, we can assume that women were given priority during the rescue.
* **Embarked Feature:** Embarked indicates from which port the passengers boarded the ship. Men from 3rd class predominantly embarked from Southampton. Passengers embarked from Cherbourg has highest survival rate. The reason of it, most men are from the 1st class and the number of women is more than men.
* **Cabin Feature:** This feature has most NaN values at total. At first NaN values are filled with N class to process. Then, because of not NaN values are unique and their first letter represents their belonged deck only first characters of the cabin data are going to be considered.
* **Name Feature:** 2 Main features are going to be obtained from the name feature. These are passengers title and their surname. From their titles their status, age, survive relevant information can be obtained. From their surnames they can be grouped to match missing Cabin features.
* **Parch & SibSp Features:** Parch indicates the number of parents in the family, while SibSp indicates the number of spouses and siblings. In order to determine the number of people in the family and to make generalizations, we combine these two columns to create a new feature that indicates how many people the family consists of.
* **Ticket Feature:** Passengers who have same ticket means they bought these tickets as a group. It shows these groups may not be the family but friends. This feature shows us again if the passenger is alone or with a high group s/he has low survival rate.
* **Fare Feature:** At first, it is normalized with interquartile ranges. Then, distribution boundaries obtained with qcut, but because of I will be using tree based models at submission it is not processed. 
* **Pclass Feature:** This feature is ordinal categorical data. It shows the class of the passenger which is correlated with Fare feature. Yet, instead of keeping the categorical ordinal as same, categorizing it increased the overall succes at train & test side. 
* **Age Feature:** Survival rate of children is particularly high. Most of the boarders are in the 18-40 age range.
## 2.2 Feature Correlations
<img src="https://user-images.githubusercontent.com/45767042/153708144-b3ff4f2d-8d81-41c0-b704-5fcbebab35e8.png">

## 2. Train & Evaluation
## 2.1 CATBoost Classifier
* **Depth:** Determines the depth of the tree and is the same for all trees.
* **Iterations:** Determines the maximum number of trees to be created.
* **Learning Rate:** It is the weight regulation coefficient against the error made.
* **l2_leaf_reg:** L2 regulation cost function coefficient.
* **leaf_estimation_method:** It is a method of calculating the values inside the leaves.
## 2.2 Feature Importance
Feature importance indicates how much importance the trained machine learning model gives to which features when deciding on a output. Like correlation matrices, feature importance also helps us to understand the connections between features and output. Thus, we can analyze these data by understanding which outputs the machine learning model gives importance to and which does not.
<img src="https://user-images.githubusercontent.com/45767042/153707973-2646d6b7-fa34-4f03-ab9f-59cc9a5a862c.png">

## 3. Submission
After evaluating the performance of the Submission models alone and together, I got the most successful result with **CatBoost**. In this evaluation, I provided the estimation of the submission data from underfit to overfit with StratifiedKFold. With this module, I have been trained by subtracting 20% each time from the data set and assigned the probabilities of the predictions made as a result of that training to the columns. Finally, I took the average of these probabilities and decided whether that person was survived or not.
