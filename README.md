# <p align="center"> Drinker & Smoker Classification </p>

## <p align="center"> Introduction </p>
<p align="justify"> This classification project aims to compare and select best fitted models in predicting whether a person is a drinker or a smoker according to some body signals. This project comprises four major components. Firstly, data summary and pre-process. Next, exploratory data analysis (EDA) is conducted to explore and display the distribution of responses and predictors. Descriptive summary, correlation heatmap, QQ-plots and histogram plots are employed to conduct distribution, correlation and normality check. </p>

<p align="justify"> Then, 11 appropriate models we have learned in Math 251 are employed firstly fit and test on sample data and finally on the whole data, including K-Nearest Neighbors (KNN), Logistic Regression (LR), Linear Discriminant Analysis (LDA), Quadratic Discriminant Analysis (QDA), Naïve Bayes (NB), Decision Tree (DTree), Bootstrap Aggregation (Bagging), Random Forest Classifier (RFC), Gradient Boosting Classifier (GBC), Support Vector Machines (SVM) and Artificial Neural Networks (ANN). Finally, test error rate and computing time are used as major criterion to compare and select the best fitted model to predict drinker & smoker. </p>

## 1. Data and Pre-process
<p align="justify"> The data to be used is collected from the National Health Insurance Service in Korea. I obtain it from Kaggle.com . It has 991,346 observations, 18 quantitative variables and 6 qualitative variables. There is no missing value. To clean the data, I remove 26 duplicated observations; remove 57 observations in which variable ‘waistline’ is 999 cm; change value 9.9 in variable sight_left and sight_right to be 0, which means blind. Consequently, the clean data has 991,263 observations. Furthermore, I standardize the quantitative predictors, and convert categorical values of qualitative predictors to numerical values. </p>

## 2. Exploratory Data Analysis (EDA)
1. **Response y.** There are two Response y, ‘drinker’ and ‘smoker’. ‘drinker’ has two classes that 50.99% observations are in class 0 (Not Drink) and 49.01% are in class 1 (Drink). The distribution of ‘drinker’ across two classes are balanced. ‘smoker’ has three classes that 60.95% observations are in class 0 (Never Smoke), 17.35% are in class 1 (Previously Smoke), and 21.70% are in class 2 (Actively Smoke). The distribution of ‘smoker’ across its three classes are not balanced. (See Figure 1) </p>

<p align="center"> <img width="45%" alt="Screen Shot 2024-01-31 at 3 59 46 PM" src="images/Drinker histogram.png">
                   <img width="55%" alt="Screen Shot 2024-01-31 at 3 59 46 PM" src="images/Smoker histogram.png"> </p>
<p align="center"> Figure 1 Histogram Distribution of Response y </p>

2. **Quantitative Predictors.** There are 18 quantitative predictors including age, weight, height, waistline, eye sights and some commonly used blood test results. Table 1 gives the descriptive summary of each quantitative predictor, including predictor’s name, definition, mean, standard deviation, minimum & maximum value, 25%, 50% and 75% quartile value. Meanwhile, I examine the histogram distribution of the quantitative predictors (See Figure 2 & 3). It is found that BLDS, tot_chole, HDL_chole, LDL_chole, triglyceride, hemoglobin, serum_creatinine, SGOT_AST, SGOT_ALT and gamma_GTP have extreme large outliers and are heavily skewed by a long right tail. This implies a certain level of violation of normal distribution. </p>

<p align="center"> <img width="98%" alt="Screen Shot 2024-01-31 at 4 06 47 PM" src="https://github.com/xiangyaosjsu/Math-251-Project/assets/145530232/00a0b888-6df8-4479-bdd6-0f89e3de3b5e"> </p>
<p align="center"> Table 1 Descriptive Summary of Quantitative Predictors </p>

<p align="center"> <img width="98%" alt="image" src="images/Quantitative Histogram.png"> </p>
<p align="center"> Figure 2 Histogram Distribution of Quantitative Predictors </p>

<p align="center"> <img width="98%" alt="image" src="images/HDL Full vs Small.png"> </p>
<p align="center"> Figure 3 HDL_chole Distribution: Full Range vs. Smaller Range </p>

<p align="justify"> Moreover, I use correlation heatmap to check the correlation among quantitative predictors. It is found that among the 18 quantitative predictors, 8 pairs have moderate to strong correlation coefficients ([0.5,0.88]). Please see Appendix III for Correlation Heatmap & specific correlation coefficients. The correlations between quantitative predictors might affect some classification models’ prediction performance, such as NB & Random Forest. Because NB assumes independence among predictors within each class and Random Forest has a decorrelation process. </p>

![Correlation heatmap](https://github.com/xiangyaosjsu/Math-251-Project/assets/145530232/0e6be5a7-066f-4808-96c6-ddbbfc20c3b7)
<p align="center"> Figure 4 Correlation Heatmap </p>


<p align="justify"> Furthermore, I use QQ-plot to do normality check (See Appendix IV). Whether or not normal distribution assumption of features is satisfied would have an impact on the prediction performance of LDA & QDA. Some predictors, including age, height, weight, waistline, sight_left, sight_right, SBP, DBP and hemoglobin is somewhat alike a normal bell curve shape; however, other predictors, including BLDS, tot_chole, HDL_chole, LDL_chole, triglyceride, serum_creatinine, SGOT_AST, SGOT_ALT and gamma_GTP is totally different from normal distribution shape. Thus, normality assumption is violated in some features. I think it is the extreme large outliers stretch those predictors’ distribution shapes to the far right. 

<p align="justify"> (3) Qualitative Predictors. Three qualitative variables are included into the models , gender, left and right hearings. There are 53.11% observations are female; 46.90% are males; 96.85% and 96.95% observations have normal left hearing and right learning, while 3.15% and 3.05% observations have abnormal left and right hearing. The distribution of left and right hearing across levels/classes are highly imbalanced. These two variables probably are not good predictors. </p>






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
