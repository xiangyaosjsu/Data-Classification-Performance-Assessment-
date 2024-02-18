![image](https://github.com/xiangyaosjsu/Math-251-Project/assets/145530232/03efefea-97f4-4401-b96a-362dd477aec4)# <p align="center"> Drinker & Smoker Classification </p>

## <p align="center"> Introduction </p>
<p align="justify"> This classification project aims to compare and select best fitted models in predicting whether a person is a drinker or a smoker according to some body signals. This project comprises four major components. Firstly, data summary and pre-process. Next, exploratory data analysis (EDA) is conducted to explore and display the distribution of responses and predictors. Descriptive summary, correlation heatmap, QQ-plots and histogram plots are employed to conduct distribution, correlation and normality check. </p>

<p align="justify"> Then, 11 appropriate models we have learned in Math 251 are employed firstly fit and test on sample data and finally on the whole data, including K-Nearest Neighbors (KNN), Logistic Regression (LR), Linear Discriminant Analysis (LDA), Quadratic Discriminant Analysis (QDA), Naïve Bayes (NB), Decision Tree (DTree), Bootstrap Aggregation (Bagging), Random Forest Classifier (RFC), Gradient Boosting Classifier (GBC), Support Vector Machines (SVM) and Artificial Neural Networks (ANN). Finally, test error rate and computing time are used as major criterion to compare and select the best fitted model to predict drinker & smoker. </p>

## 1. Data and Pre-process
<p align="justify"> The data to be used is collected from the National Health Insurance Service in Korea. I obtain it from Kaggle.com [^1]. It has 991,346 observations, 18 quantitative variables and 6 qualitative variables. There is no missing value. To clean the data, I remove 26 duplicated observations; remove 57 observations in which variable ‘waistline’ is 999 cm; change value 9.9 in variable sight_left and sight_right to be 0, which means blind. Consequently, the clean data has 991,263 observations. Furthermore, I standardize the quantitative predictors, and convert categorical values of qualitative predictors to numerical values. </p>

## 2. Exploratory Data Analysis (EDA)
**(1) Response y.** There are two Response y, ‘drinker’ and ‘smoker’. ‘drinker’ has two classes that 50.99% observations are in class 0 (Not Drink) and 49.01% are in class 1 (Drink). The distribution of ‘drinker’ across two classes are balanced. ‘smoker’ has three classes that 60.95% observations are in class 0 (Never Smoke), 17.35% are in class 1 (Previously Smoke), and 21.70% are in class 2 (Actively Smoke). The distribution of ‘smoker’ across its three classes are not balanced. (See Figure 1)

<p align="center"> <img width="47%" alt="Screen Shot 2024-01-31 at 3 59 46 PM" src="images/Drinker histogram.png">
                   <img width="52%" alt="Screen Shot 2024-01-31 at 3 59 46 PM" src="images/Smoker histogram.png"> </p>
<p align="center"><b>Figure 1. Histogram Distribution of Response y</b></p>

**(2) Quantitative Predictors.** There are 18 quantitative predictors including age, weight, height, waistline, eye sights and some commonly used blood test results. Table 1 gives the descriptive summary of each quantitative predictor, including predictor’s name, definition, mean, standard deviation, minimum & maximum value, 25%, 50% and 75% quartile value. Meanwhile, I examine the histogram distribution of the quantitative predictors (See Figure 2 & 3). It is found that BLDS, tot_chole, HDL_chole, LDL_chole, triglyceride, hemoglobin, serum_creatinine, SGOT_AST, SGOT_ALT and gamma_GTP have extreme large outliers and are heavily skewed by a long right tail. This implies a certain level of violation of normal distribution.

<p align="center"> <img width="98%" alt="Screen Shot 2024-01-31 at 4 06 47 PM" src="https://github.com/xiangyaosjsu/Math-251-Project/assets/145530232/00a0b888-6df8-4479-bdd6-0f89e3de3b5e"> </p>
<p align="center"><b> Table 1. Descriptive Summary of Quantitative Predictors </b>b</p>

<p align="center"> <img width="98%" alt="image" src="images/Quantitative Histogram.png"> </p>
<p align="center"><b> Figure 2. Histogram Distribution of Quantitative Predictors </b></p>

<p align="center"> <img width="98%" alt="image" src="images/HDL Full vs Small.png"> </p>
<p align="center"><b> Figure 3. HDL_chole Distribution: Full Range vs. Smaller Range </b></p>

<p align="justify"> Moreover, I use correlation heatmap to check the correlation among quantitative predictors. It is found that among the 18 quantitative predictors, 8 pairs have moderate to strong correlation coefficients ([0.5,0.88]). Please see Figure 4 for Correlation Heatmap & specific correlation coefficients. The correlations between quantitative predictors might affect some classification models’ prediction performance, such as NB & Random Forest. Because NB assumes independence among predictors within each class and Random Forest has a decorrelation process. </p>

<p align="center"> <img width="80%" alt="image" src="images/Correlation Heatmap.png"> </p>
<p align="center"><b> Figure 4. Correlation Heatmap </b></p>

<p align="center"> <img width="70%" alt="image" src="images/Table 2.png"> </p>
<p align="center"><b>Table 2. Correlation Coefficients (>= 0.50) of Quantitative Predictors</b></p>

<p align="justify"> Furthermore, I use QQ-plot to do normality check (See Figure 5). Whether or not normal distribution assumption of features is satisfied would have an impact on the prediction performance of LDA & QDA. Some predictors, including age, height, weight, waistline, sight_left, sight_right, SBP, DBP and hemoglobin is somewhat alike a normal bell curve shape; however, other predictors, including BLDS, tot_chole, HDL_chole, LDL_chole, triglyceride, serum_creatinine, SGOT_AST, SGOT_ALT and gamma_GTP is totally different from normal distribution shape. Thus, normality assumption is violated in some features. I think it is the extreme large outliers stretch those predictors’ distribution shapes to the far right. 

<p align="center"> <img width="98%" alt="image" src="images/QQ-plot.png"> </p>
<p align="center"><b> Figure 5. QQ-plot of Quantitative Indicators </b></p>

**(3) Qualitative Predictors.** Three qualitative variables are included into the models, gender, left and right hearings. There are 53.11% observations are female; 46.90% are males; 96.85% and 96.95% observations have normal left hearing and right learning, while 3.15% and 3.05% observations have abnormal left and right hearing. The distribution of left and right hearing across levels/classes are highly imbalanced. These two variables probably are not good predictors. </p>

## 3. Model Training and Parameter Selection. 
<p align="justify"> The whole data set has about 1 million observations. Directly doing model training and parameter tuning on the whole data will cost a great amount of time. Thus, I start from using sample data to select some manifestly better classification models and their corresponding best parameters. Then, apply the selected model and best parameters to the whole data set to do model comparison and select the best fitted model. (See Figure 6 for Model fit and selection process) </p>

<p align="center"> <img width="80%" alt="image" src="images/Model Fit Process.png"> </p>
<p align="center"><b> Figure 6. Model Fit and Selection Process </b></p>

<p align="justify"><b>Step 1. Use Sample Data to Select Models & Parameters. Firstly, Draw Random Samples.</b> From the original clean data, I randomly draw two samples. In each sample, there is one training data set and 50 test data sets. The training data in sample 1 has 10k observations, which is equivalently to about 1% of the whole data; each test data set has 1k observation. The training data in sample 2 has 100k observations, which is equivalently to about 10% of the whole data; each test data set has 5k observations. For each sample, I firstly randomly sample the training data set from the original clean data. Then, I randomly draw 50 test data sets with replacement from “original clean data – training data of that sample”, such that the training and test data in each sample don’t have an overlap. </p>

<p align="justify">The reasons to draw two samples is that sample 1 uses about 1% observations to fit model. The computing time is reasonably good, but the representation of the data is not that trustworthy. Sample 2 uses about 10% observations to fit model. The representation is more trustworthy; however, it takes more than 10 hours for some models to finalize model fit. Therefore, I use both samples to fit the 10 classification models and find their best parameters. Based on the two lists of selected models and best parameters, a final list of selected models and best parameters are determined. </p>

<p align="justify"><b> Secondly, Model Fit. </b> 10 classification models that we have learned in Math 251 which are applicable to tabular data are used to fit models. They are KNN, LR, LDA, QDA, NB, DTree, Bagging, RFC, GBC, SVM and ANN (Full model names are listed in Introduction). Among them, LR, LDA, QDA, NB & Bagging use fixed parameters. KNN, DTree, Random Forest, Boosting and SVM select the best parameters through employing grid search to do parameter tuning. I set CV=10 which means I employ k-folder cross validation method (k=10) to select best parameters. I use ‘decision_function_shape’ = ‘ovo’ so that SVM model could do multi-class classification & prediction. Considering ANN takes relatively long time to fit model, the best parameter selection is only done based on sample 1 using generated variable smoker_drinker  as response. The best parameters selected from what I have tried for ANN are layers = 4, neurons=[500, 400, 200, 100], p=0.5, epoch=300. Then, all ANN models use these selected best parameters to train model. Please see Figure 3 for parameters used in grid search and the process to select models and best parameters using sample data. Besides, I set random_state=1 for KNN, DTree, Bagging, RFC, GBC & SVM.</p>

<p align="center"> <img width="80%" alt="image" src="images/Model Selection.png"> </p>
<p align="center"><b> Figure 7. Model Fit and Selection Process </b></p>




[^1]: https://www.kaggle.com/datasets/sooyoungher/smoking-drinking-dataset?resource=download
[^2]: In the original data set, there is another qualitative variable which is urine_protein with six levels. But I don’t use it to fit model. All other variables are employed by this project. 
[^3]: This is a generated variable based on original response drinker & smoker. Firstly, I change ‘smoker’ from 3-level to be 2-level through combining level 1 (Previously smoke) & 2 (Actively smoke) of smoker to be level 1 (Smoker). Then, based on 2-level ‘smoker’ & ‘drinker’, I created variable ‘smoker_drinker’ with 4 levels. Level 0 = Not smoke & Not drink; Level 1 = Smoke, Not drink; Level 2 = Not smoke, Drink; Level 4 = Smoker & Drink. 
