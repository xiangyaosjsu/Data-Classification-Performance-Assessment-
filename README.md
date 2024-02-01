# <p align="center"> Drinker & Smoker Classification </p>

## <p align="center"> Introduction </p>
<p align="justify"> This classification project aims to compare and select best fitted models in predicting whether a person is a drinker or a smoker according to some body signals. This project comprises four major components. Firstly, data summary and pre-process. Next, exploratory data analysis (EDA) is conducted to explore and display the distribution of responses and predictors. Descriptive summary, correlation heatmap, QQ-plots and histogram plots are employed to conduct distribution, correlation and normality check. </p>

<p align="justify"> Then, 11 appropriate models we have learned in Math 251 are employed firstly fit and test on sample data and finally on the whole data, including K-Nearest Neighbors (KNN), Logistic Regression (LR), Linear Discriminant Analysis (LDA), Quadratic Discriminant Analysis (QDA), Naïve Bayes (NB), Decision Tree (DTree), Bootstrap Aggregation (Bagging), Random Forest Classifier (RFC), Gradient Boosting Classifier (GBC), Support Vector Machines (SVM) and Artificial Neural Networks (ANN). Finally, test error rate and computing time are used as major criterion to compare and select the best fitted model to predict drinker & smoker. </p>

## 1. Data and Pre-process
<p align="justify"> The data to be used is collected from the National Health Insurance Service in Korea. I obtain it from Kaggle.com . It has 991,346 observations, 18 quantitative variables and 6 qualitative variables. There is no missing value. To clean the data, I remove 26 duplicated observations; remove 57 observations in which variable ‘waistline’ is 999 cm; change value 9.9 in variable sight_left and sight_right to be 0, which means blind. Consequently, the clean data has 991,263 observations. Furthermore, I standardize the quantitative predictors, and convert categorical values of qualitative predictors to numerical values. </p>

## 2. Exploratory Data Analysis (EDA)
<p align="justify"> (1) Response y. There are two Response y, ‘drinker’ and ‘smoker’. ‘drinker’ has two classes that 50.99% observations are in class 0 (Not Drink) and 49.01% are in class 1 (Drink). The distribution of ‘drinker’ across two classes are balanced. ‘smoker’ has three classes that 60.95% observations are in class 0 (Never Smoke), 17.35% are in class 1 (Previously Smoke), and 21.70% are in class 2 (Actively Smoke). The distribution of ‘smoker’ across its three classes are not balanced. (See Figure 1) </p>

<p align="center"> <img width="569" alt="Screen Shot 2024-01-31 at 3 59 46 PM" src="https://github.com/xiangyaosjsu/Math-251-Project/assets/145530232/40e9cc66-65ee-4252-9369-0297eb00e964"> </p>
<p align="center"> Figure 1 Histogram Distribution of Response y </p>






## 3. Variables
### (1) Response Variable (y): 
- Smoking status: SMK_stat_type_cd [3 levels: 1(never), 2(used to smoke but quit), 3(still smoke)]
- Drinking status: DRK_YN	[2 levels: Drinker or Not]
- Smoking & Drinking status: will be generated based on Smoking status and Drinking status with 6-levels

### (2) Predictors (x): 
####     I. Quantitative Predictors:
- age:	round up to 5 years
- height:	round up to 5 cm[cm]
- weight:	[kg]
- waistline: [cm]
- sight_left:	eyesight(left)
- sight_right:	eyesight(right)
- SBP:	Systolic blood pressure[mmHg]
- DBP:	Diastolic blood pressure[mmHg]
- BLDS:	BLDS or FSG(fasting blood glucose)[mg/dL]
- tot_chole:	total cholesterol[mg/dL]
- HDL_chole:	HDL cholesterol[mg/dL]
- LDL_chole:	LDL cholesterol[mg/dL]
- triglyceride:	triglyceride[mg/dL]	
- hemoglobin:	hemoglobin[g/dL]
- serum_creatinine:	serum(blood) creatinine[mg/dL]
- SGOT_AST:	SGOT(Glutamate-oxaloacetate transaminase) AST(Aspartate transaminase)[IU/L]
- SGOT_ALT:	ALT(Alanine transaminase)[IU/L]	
- gamma_GTP:	y-glutamyl transpeptidase[IU/L]

####     II. Qualitative Predictors:
- Sex:	male, female
- hear_left:	hearing left, 1(normal), 2(abnormal)
- hear_right:	hearing right, 1(normal), 2(abnormal)
- urine_protein:	protein in urine, 1(-), 2(+/-), 3(+1), 4(+2), 5(+3), 6(+4)
