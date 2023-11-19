# Heart-Disease-Detection---Regression-Model-Analysis

The topic of our project is to study the factors that influence the 10-year risk of future coronary heart disease (CHD). The research question is how gender, diabetes, age, cigarette usage, total cholesterol level, systolic blood pressure, Body Mass Index (BMI), and glucose level affect CHD? We obtained raw data on CHD from Kaggle, and analyzed the data using R. We applied EDA analysis on each potential predictors, and fit multiple logit regression lines between CHD and statistically significant predictors. The final reaching equation is

<img width="883" alt="Screen Shot 2023-11-18 at 11 48 23 PM" src="https://github.com/JessicaaaJe/Heart-Disease-Detection---Regression-Model-Analysis/assets/94040700/8a155be6-653b-49be-8a3b-b17debbc39e1">

## Introduction
We are interested in evaluating the potential factors of heart disease because it causes 12 million deaths every year worldwide. If we could find the relationship between potential factors and heart disease, it could help to predict the group of people who are more likely to have heart disease. With that information, we can then apply treatment to them at the early stage of the disease.

## Dataset
We found the dataset in Kaggle (https://www.kaggle.com/datasets/dileep070/heart-disease-prediction-using-logistic-regression)). 
This dataset randomly collects 4000 people’s information about the CHD in the town of Framingham, Massachusetts. The dataset is from an ongoing cardiovascular study in Massachusetts. We consider 4000 to be a little large as sample size, so we randomly select 500 to analyze.
#### The processed dataset has been put in the repository. 

The 10-year risk of future coronary heart disease (CHD), which indicates whether a person is going to have heart disease in 10 years, is the response variable. In CHD, 1 means yes: a person has a ten-year risk of coronary heart disease; 0 means no: a person does not have a ten- year risk of coronary heart disease. The 8 explanatory variables are categorized into two sets: Numerical and Categorical. With these 8 explanatory variables, we need to find out which explains the variance in CHD and what is the mathematical relationship between CHD and these variables.

## Methodology

The dataset gives a sample data of size 4200+ with the response variable ten-year risk of coronary disease (TenYearCHD) and 15 other possible predictors. We filter the data and delete the ones that are marked as N/A which are overall 500+. And then we get valid data 3600+. And then we assign each row a random number, rank them ascendingly, and get the first 500 sample data to be used in our analysis. From the 15 predictors, we choose 9 of them which have the most completed data. Two of them are categorical: gender and diabetes. Gender is categorized into male and female. Male is represented by 1, and female is defined as the baseline 0. For diabetes, people who have diabetes are indicated by 1. And people who do not have diabetes are indicated by 0. There are other 7 numerical predictors: age, cigsPerDay(the number of cigarettes that the person smoked on average in one day), totChol(total cholesterol level), sysBP(systolic blood pressure),BMI(Body Mass Index), heartRate, glucose are numeric data.
After being clear of what are the response variables and the predictors, we apply EDA(exploratory data analysis) on each predictors by drawing empirical logit plots on the numerical predictors and a mosaic plots on the categorical predictors. There are a total 7
predictors we consider to fit the multiple logistic regression model: two categorical data: gender and diabetes. Male indicates a higher possibility of having the 10 year risk of coronary disease than female. People who have diabetes also have a higher possibility of having the risk. And there are other five numerical predictors. The log odds indicate a positive relation to age, cigsPerDay, log(totChol), sysBP, and log(glucose). The empirical logit plot of BMI to log(odds) and heartRate to log(odds) does not indicate a strong relationship between the response variable and predictors, therefore we do not consider these two variables as potential factors affecting TenYearCHD. Plus, the independence and randomness of the data is ensured from the sampling of the data.
To avoid the correlation between each variable which may affect the accuracy of the multilogistic model, we draw a 5*5 matrix to check the dependency of five numerical variables. As shown in the figure, no correlation coefficient between two variables exceeds 0.5. Therefore, no interaction term needs to be added.

<img width="777" alt="Screen Shot 2023-11-18 at 11 50 42 PM" src="https://github.com/JessicaaaJe/Heart-Disease-Detection---Regression-Model-Analysis/assets/94040700/a84561d3-15d9-46ad-9585-59d94f368478">

We then use the BSS function in R, and 7 predictors above to derive the best model for multiple logistic regression. From the Figure1 final model, there are five factors chosen in the best model. The AIC of this model is 403.9. From the coefficient information, we can write

down the equation of the multiple logistic regression line to be log(odds) = -13.764 + 0.72 gender +0.08 age +0.01cigsPerDay + 1.15 log(glucose).

<img width="873" alt="Screen Shot 2023-11-18 at 11 51 15 PM" src="https://github.com/JessicaaaJe/Heart-Disease-Detection---Regression-Model-Analysis/assets/94040700/5522760c-af34-47dd-9e86-354cd525857f">

To make sure the final model is effective, we’d better check a few other models with more predictors in it. The first model we choose to compare is the whole model which includes all the 7 predictors. We use a nested likelihood ratio test to compare the fitness of these two models. From figure2, we can see the probability is 0.2862, which is much bigger than the one to successfully reject the null hypothesis. Therefore, we stick with the final model. We can also check the AIC of the final model and the whole model. Final model AIC is 403.89, whole model AIC is 405.39. As smaller AIC is preferred, the final model is chosen.
<img width="910" alt="Screen Shot 2023-11-18 at 11 51 47 PM" src="https://github.com/JessicaaaJe/Heart-Disease-Detection---Regression-Model-Analysis/assets/94040700/3904b15e-7e6f-4d19-a156-19cb3be4ce06">

Another model, which is named in R as the third model is chosen to compare with the final model. It adds one more predictor- log(totChol) to the final model. The same nested likelihood ratio test is performed on the final model and third model. From figure 3, we can see the probability is 0.1591 which is larger than the one that can reject the final model. Therefore, we still prefer the final model.
<img width="926" alt="Screen Shot 2023-11-18 at 11 52 21 PM" src="https://github.com/JessicaaaJe/Heart-Disease-Detection---Regression-Model-Analysis/assets/94040700/0c9dc0f4-e41b-4dcc-b24e-f8aa7f2aeab7">

## Analysis and Result
All of our analysis is completed by using R, and the packages we used include matrix, bestglm, and ggplot2. In our process of analyzing the relation between CHD and the potential variables, We drew empirical logit plots on the numerical predictors and a mosaic plots on the categorical predictors.
The model we chose was as follows:
<img width="840" alt="Screen Shot 2023-11-18 at 11 52 49 PM" src="https://github.com/JessicaaaJe/Heart-Disease-Detection---Regression-Model-Analysis/assets/94040700/60dc6299-cff1-4cfa-b439-d6f844b29028">

It’s the best fitted model because it has the smaller AIC. Final model’s AIC is 403.89, whole model AIC is 405.39. Therefore, we chose to use the final model.
Speaking of the performance of our final model, we think it fits our assumption that CHD is affected by a number of regressors. Although we only included five predictors in our final

model, we still proved in the first part that all those predictors are influencing CHD. We chose the best model with predictors being statistically significant.

<img width="486" alt="Screen Shot 2023-11-18 at 11 53 18 PM" src="https://github.com/JessicaaaJe/Heart-Disease-Detection---Regression-Model-Analysis/assets/94040700/a480e5bf-abca-4d7d-8587-d518acbcfeb8">


Assuming no change in other predictors, we are 95% confident that Male is estimated to be on the range between 0.26027 to 1.18427, age is estimated to be on the range between 0.05699 to 0.11345, CigsPerDay is estimated to be in the range between 0.00521 to 0.04238, sysBP is estimated to be in the range between 0.005966 to 0.02517, log (glucose) is estimated to be in the range between 0.36214 to 1.950412.
Holding everything else constant, on average, compared with females, males are 0.717 more likely to have CHD. Holding everything else constant, on average, one year increase in age will lead to 0.085 more likely to have CHD. Holding everything else constant, on average, one unit increase in CigsPerDay will lead to 0.024 more likely to have CHD. Holding everything else constant, on average, one year increase in sysBP will lead to 0.016 more likely to have CHD. Holding everything else constant, on average, one year increase in log (glucose) will lead to 1.147 more likely to have CHD.


## Conclusion
By doing a thorough and comprehensive analysis of the datasets of CHD using seven different variables, we came up with a model that could predict the likelihood of having CHD using relevant regressors. In the process of building a model, we chose the best model with less regressors, and lower AIC could make the best prediction.
In the beginning of our research, we aim to find factors that affect the probability of having CHD. The model includes five major factors that are significant to the prediction of having CHD, one categorical variable and four numeric variables. Our research is useful because it could provide some helpful insights about the prediction and estimation of having CHD. It can be used in medical as well as health policy areas in the future.


