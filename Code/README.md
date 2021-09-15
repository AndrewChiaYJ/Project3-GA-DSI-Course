# Codes Sequence

### **Do read the codes in the order below, so as to understand better on the codes and thought process.**


**1) Part 1 -  P. Statement, Background, Data Collection, Data Cleaning, NLP, and EDA**


This code is to state the problem statement and background of the project. 


Followed by collecting data via API, to pull contents of posts of 2 different subreddit and store them into dataframes, 1st is /r/stocks and 2nd is /r/CryptoCurrency.

Then, processes are being done to cleaning both the dataframes, merge them together, and then further cleaning using the Natural Language Processing techniques is being done.

It is followed by multiple EDAs done to understand the dataset better.

Lastly, a final dataset.csv is being saved for usage in Part 2.


**2) Part 2 - Modelling, Model Evaluation, Recommendations and Future Steps**


This code is to do modelling process on the data. We have 4 combinations of modelling being done:
1. Multinomial Naive Bayes Model using dataframe from Count Vectorization
2. Multinomial Naive Bayes Model using dataframe from TF-IDF Vectorization
3. Logistic Regression Model using dataframe from Count Vectorization
4. Logistic Regression Model using dataframe from TF-IDF Vectorization

Based on accuracy score and recall score, Logistic Regression Model using dataframe from TF-IDF Vectorization has the highest of both scores, hence chosen for model evaluation.

Then model evaluation is then done and confusion matrix of the model is being printed. 

Lastly, recommendations and future steps of this project.


**3) Appendix - Data Dictionary**


This code is the data dictionary for all the variables in the final dataset, for better understanding of what the items in the excel dataset mean.