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
  
- 1 value where stroke = 0 and gender = 'Other' (leaving two classes - Male & Female)  
- 