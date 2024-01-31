# Drinker & Smoker Classification

## 1. Project Description
**Project**: Smoking and Drinking Classification

**Project Target**: predict whether a person is a smoker and/or a drinker according to body signals. 
- Models/methods: based on data character, I would apply different and applicable methods/models to predict smoker, drinker, smoker & drinker respectively using body signal variables.
- EDA: to present the distribution and characteristics of each variable; also relationship between/among variables, such as correlation. 
- Prediction performance will be compared across models to choose a best model for different response y.
- Various data visualization methods would be applied to assist in presenting analysis results.

## 2. Data
**Data**: Smoking and Drinking Dataset with body signal. The dataset is collected from the National Health Insurance Service in Korea. 

**Data Source**: https://www.kaggle.com/datasets/sooyoungher/smoking-drinking-dataset?resource=download

[Professor, the data size is big and I failed to uploda it into GitHub repository. I am learning and will figure it out soon. For now, please lick on this link to get the original data. Many thanks!]

**Number of Features**: 24 (6 Qualitative variables; 18 Quantitative variables) [Might not use all variables for the project]

**Number of Observations**: 991,346

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
