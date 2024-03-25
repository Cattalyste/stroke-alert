# stroke-alert

**Predictable variable: stroke**  
  
We are aiming to early predict and alert the stroke risk based on individual's demographical and health data.  
  
### Original data
  
Original dataframe consists of 5110 lines and 12 columns. Predictable stroke class is highly imbalanced.
  
Data columns:
1 independent variable **stroke**,  
10 dependent variables (excluding *id*):  
- 3 continuous variables - **age**, **bmi**, **avg_glucose_level**  
- 7 categorical variables:  
  - 2 binary variables - **hypertension**, **heart_disease**
  - 5 nominal variables - **gender**, **ever_married**, **work_type**, **Residence_type**, **smoking_status**  
  
**Data has missing bmi and smoking_status values.**  

### Data cleaning  
  
- Gender: 1 value where stroke = 0 and gender = 'Other' (leaving two classes - Male & Female)   
  
- Age: Minimum age for stroke excluding outliers is 32 years old. To balance the predictable variable classes, dataset was trimmed to contain the age from year 30. Several logistic regression tests were performed to evaluate the dataset performance when taking more records (removing records up to age 20) or less records (removing records up to age 32) but this deteriorated the model results.  
  
- Smoking status: 620 records deleted where smoking_status is Unknown and stroke class is negative to get rid of the missing values and balance out predictable classes.  
  
- BMI: BMI greater than 50 is not realistic for the vast majority of individuals and are clearly outliers in the dataframe. BMI values under 15 when age is > 30 is not realistic as well. So, these records were deleted.   
  
- Ever married: column deleted since the two variables - age and ever_married are highly associated (13% of correlation, p-value = 0).  
  
- Average glucose level: range (55.12 - 271.74) is realistic.
  
  
### Data imputation  
  
- BMI values were imputed while grouping data features and replacing the null BMI value with the mean value of the group where NaN is present. Continuous variables were grouped by their distrbution by minimum logical number of bins to respect the obesity type or age / glucose level groups. Firstly all features were used for grouping, then the groups were enlarged by taking one feature out (that has least impact to the stroke prediction based on correlation & association tests results) of the grouping criteria. This was done recursively to fill out all missing BMI values.  
  
- Smoking status were imputed in two different ways. First is similar to BMI values imputation method and this deteriorated the results.  
  
  
### Supervised Classification Algorithms used 
  
- Random Forest Classifier - Utilizes an ensemble of decision trees to make predictions, offering robustness against overfitting and high accuracy in classification tasks.
  
- Logistic Regression - A linear model used for binary classification, estimating the probability of a binary outcome based on input features through a logistic function.
  
- Voting Classifier - Combines predictions from multiple individual classifiers to make a final prediction, leveraging the wisdom of crowds for improved classification accuracy.
  
  
### Results
  
The most important evaluation criteria in this case is Positive stroke class Recall as in the medical domain it is sensitive to correctly predict the occurrence of strokes. High recall ensures that a large proportion of actual stroke cases are correctly identified by the model, reducing the likelihood of false negatives and potentially enabling timely interventions or treatments to prevent strokes.
  
The **multiple features Voting Classifier** yielded the best results - 88% of recall in positive stroke class.  
  
While the results show that model performs relativelly well statistically, in the health sector such prediction would mean that at least 1 of 10 predictions are False. The situation could be improved by revealing the prediction probability of the stroke class. If the prediction is around 50%, more data should be collected to give the more confident prediction.