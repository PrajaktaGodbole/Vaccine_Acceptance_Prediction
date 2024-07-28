# Vaccine_Acceptance_Prediction
Our goal is to predict how likely individuals are to receive their H1N1 and seasonal flu vaccines
based on past data of 2009. Specifically, predicting two probabilities: one for h1n1_vaccine and 
one for seasonal vaccine. The labels are target variables i.e. h1n1 vaccine and seasonal vaccine 
whereas the 35 features are all the components related to the probability of people for the target 
variable. The evaluation metric is ROC AUC accuracy.

# Approach 
Exploration: There were 26707 rows, 35 features for the dataset and labels data were 26707 rows and 2 columns for target variables. Initially we preview the dataset, columns data types, proportion of vaccines taken by people where 21.2 % took h1n1 vaccine and 46.6% took the seasonal vaccine which suggests that a greater number of people take the seasonal vaccine. There are 23 numeric features, and the remaining are categorical columns.
# Finding relationship: Plot the correlation between the naturally obvious features like concern for h1n1 to know that it is positively related with the uptake of the h1n1 vaccine.
Correlation between the several types of opinions and doctor recommendations for a particular vaccine have positive correlation with taking the vaccine. Then they plot a general correlation for all the numeric columns, as shown in fig.1 which shows that opinion for vaccine effectiveness/risk and doctor recommendation plays a positive role compared to others. Other categorical variables shown in fig.2 states in general vaccine uptake is seen higher with people who are employed, above income of $75,000, female gender, married, white and age-group of 65 and older. These trends are naturally obvious and can vary through multiple regions, as time progresses, and we may see different scenarios in different regions. We focused on the numerical columns going further. 
 

# Data prep and classifier selection: 
We start with creating a pipeline to identify numeric columns, scale the data, impute the null values with median and use logistic regression because it’s a multioutput classifier as we require and widely used for binary data. We then split the data and fit the model in our training data (67%) with this pipeline and then evaluate on the remaining test data (33%) to get the AUC ROC result of 82.78% for h1n1 vaccine and 83.1% for seasonal. Then we run this model on our actual test data. We perform hyper parameter grid search using 5-fold cross validation and finding the best model that gives us higher ROC, where we get a slight increase in ROC AUC 83.1 % for h1n1_vaccine, 83.1 for seasonal vaccine.


We ran a similar pipeline for other multi output classifiers for a two group classification probability results for our target variables such as LDA, QDA, classification tree (with adjusting the hyperparameter grid) and Neural net (optimized the hidden layer). 
Then we looped over the pipeline to perform random forest, gradient boost, SVM and logistic regression to check which classifier gives higher accuracy. We found that Gradient boost gave us the highest ROC with 83.6 % for both target variables on average. Hence, we re-perform the gradient boost model to make sure we re-produce the results. So, we run this model on our actual test set and then print out the results in the required format. The below summary table gives a fair idea of all the classifiers and the resulting ROC AUC values that we performed on training set.
Sr. No.	Classifier	ROC AUC h1n1 vaccine	ROC AUC seasonal vaccine	Average
1	Logistic Regression	82.7	83.1	82.9
1.a	Logistic regression with hyper parameter grid	83.1	83.1	83.1
2	LDA	83	83	83
3	QDA	79	79	79
4	Classification tree	81.8	81.4	81.6
5	Neural net	80	81	80.5
6	Random forest			82.2
7	Gradient boost	83.7	83.4	83.6
8	SVM			83.3
Table 1: Summary of AUC values resulted by using various classifiers
Highlights and findings
1. We were excited to adjust the hyper parameter grid search for Logistic regression model and parameters in classification tree model.
2. Looping the dataset over different models to get a summarized ROC AUC list
3. Highest ROC AUC observed for Gradient boosted model
