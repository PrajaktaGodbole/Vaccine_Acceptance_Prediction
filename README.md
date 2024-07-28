# Vaccine_Acceptance_Prediction
The goal is to predict how likely individuals are to receive their H1N1 and seasonal flu vaccines
based on past data of 2009. Specifically, predicting two probabilities: one for h1n1_vaccine and 
one for seasonal vaccine. The labels are target variables i.e. h1n1 vaccine and seasonal vaccine 
whereas the 35 features are all the components related to the probability of people for the target 
variable. The evaluation metric is ROC AUC accuracy.

# Data
https://www.drivendata.org/competitions/66/flu-shot-learning/ 

# Approach 
Exploration: There were 26707 rows, 35 features for the dataset and labels data were 26707 rows and 2 columns for target variables. Initially I previewed the dataset, columns data types, proportion of vaccines taken by people where 21.2 % took h1n1 vaccine and 46.6% took the seasonal vaccine which suggests that a greater number of people take the seasonal vaccine. There are 23 numeric features, and the remaining are categorical columns.

# Finding relationship 
Plot the correlation between the naturally obvious features like concern for h1n1 to know that it is positively related with the uptake of the h1n1 vaccine.
Correlation between the several types of opinions and doctor recommendations for a particular vaccine have positive correlation with taking the vaccine. Then they plot a general correlation for all the numeric columns, as shown in correlation heatmap which shows that opinion for vaccine effectiveness/risk and doctor recommendation plays a positive role compared to others. Other categorical variables shown in distribution bar charts state in general vaccine uptake is seen higher with people who are employed, above income of $75,000, female gender, married, white and age-group of 65 and older. These trends are naturally obvious and can vary through multiple regions, as time progresses, and we may see different scenarios in different regions. Hence, focused on the numerical columns going further. 
 
# Data prep and classifier selection
Start with creating a pipeline to identify numeric columns, scale the data, impute the null values with median and use logistic regression because it’s a multioutput classifier as we require and widely used for binary data. Split the data and fit the model in our training data (67%) with this pipeline. and then evaluate on the remaining test data (33%) to get the AUC ROC result of 82.78% for h1n1 vaccine and 83.1% for seasonal. Then run this model on actual test data. Perform hyper parameter grid search using 5-fold cross validation and finding the best model that gives us higher ROC, where we get a slight increase in ROC AUC 83.1 % for h1n1_vaccine, 83.1 for seasonal vaccine.

Executed a similar pipeline for other multi output classifiers for a two group classification probability results for our target variables such as LDA, QDA, classification tree (with adjusting the hyperparameter grid) and Neural net (optimized the hidden layer). 
Looped over the pipeline to perform random forest, gradient boost, SVM and logistic regression to check which classifier gives higher accuracy, where I found that Gradient boost gave the highest ROC with 83.6 % for both target variables on average. Hence, re-perform the gradient boost model to make sure it re-produces the results. Finally, run this model on the actual test set and then print out the results in the required format. 

# Highlights and findings
1. I was excited to adjust the hyper parameter grid search for Logistic regression model and parameters in classification tree model.
2. Looping the dataset over different models to get a summarized ROC AUC list
3. Highest ROC AUC observed for Gradient boosted model
