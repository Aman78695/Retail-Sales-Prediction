# Retail-Sales-Prediction
Approach:
The approach followed here is to first check the sanctity of the data and then understand the features involved. The events followed were in our approach:

•	Understanding the business problem and the datasets.

•	Data cleaning and pre-processing: -finding null values and imputing them with appropriate values. Converting categorical values into appropriate data types and merging the datasets provided to get a final dataset to work upon.

•	Exploratory data analysis of categorical and continuous variables against our target variable.

•	Data manipulation- feature selection and engineering, feature scaling, outlier detection and treatment and encoding categorical features.

•	Modelling- The baseline model Decision tree was chosen considering our features were mostly categorical with few having continuous importance.

•	Model Performance and Evaluation

•	Store wise Sales Predictions

•	Conclusion and Recommendations

'CompetitionDistance' –

 Competition Distance is the distance in meters to the nearest competitor store. The Competition Distance distribution plot shows the distances at which generally the stores are opened

 
CompetitionDistance Distribution Plot

![download (16) (1)](https://user-images.githubusercontent.com/112580968/205921349-b2836cea-829b-4edf-80fd-4bbeb713e7c0.png)

It seems like most of the values of the CompetitionDistance are towards the left and the distribution is skewed on the right. Median is more robust to outlier effect hence median was imputed in the null values

CompetitionOpenSinceMonth- gives the approximate month of the time the nearest competitor was opened. The mode of the column is used to impute the missing values in the column as it gives the most occurring month.![download (16)](https://user-images.githubusercontent.com/112580968/205922949-9249ea4f-3022-46a5-a9f1-981889c90035.png)


CompetitionOpenSinceYear-gives the approximate year of the time the nearest competitor was opened. The mode of the column is used to impute the missing values in the column as it gives the most occurring month.

Promo2Since Week, Promo2Since Year and PromoInterval are NaN wherever Promo2 is 0 or False as can be seen in the first look of the dataset. They are replaced with 0.
Lastly before proceeding further, the two datasets were merged on the common column of 'Store' to get everything together for the analysis.

Hypothesis:-
Just by observing the head of the dataset and understanding the features involved in it, the following hypotheses could be framed: 
•	There's a feature called "DayOfWeek" with the values 1-7 denoting each day of the week. There would be a week off probably Sunday when the stores would be closed, and we would get low overall sales.

•	Customers would have a positive correlation with Sales.

•	The Store type and Assortment strategy involved would be having a certain effect on sales as well. Some premium high-quality products would fetch more revenue.

•	Promotion should be having a positive correlation with Sales.

•	Some stores were closed due to refurbishment, those would generate 0 revenue for that time period.

•	Stores are influenced by seasonality, probably before holidays sales would be high.

Correlation:

Correlation is a statistical term used to measure the degree in which two variables move in relation to each other. A perfect positive correlation means that the correlation coefficient is exactly 1. This implies that as one variable moves, either up or down, the other moves in the same direction. A perfect negative correlation means that two variables move in opposite directions, while a zero correlation implies no linear relationship at all.![download (17)](https://user-images.githubusercontent.com/112580968/205923298-d5523ec5-6ca5-4a87-a964-3d003d6f1ace.png)


•	Day of the week has a negative correlation indicating low sales as the weekends, and promo, customers and open has positive correlation.

•	State Holiday has a negative correlation suggesting that stores are mostly closed on state holidays indicating low sales.

•	CompetitionDistance showing negative correlation suggests that as the distance increases sales reduce, which was also observed through the scatterplot earlier. 

•	There's multicollinearity involved in the dataset as well. The features telling the same story as Promo2, Promo2 since week and year are showing multicollinearity.

Feature Engineering:

Some stores were closed due to refurbishment and some on account of week off or holidays. Those stores on those dates generated zero sales and hence removing the rows was important to avoid confusion by the algorithms and then removing the feature altogether because it wasn't providing any value in prediction of the sales.
There were features that like Competition Open since Month and Year. It was combined to count the total months since the nearest competition was opened.

Outlier Detection:

In statistics, an outlier is a data point that differs significantly from other observations. Outliers can occur by chance in any distribution, but they often indicate either measurement error or that the population has a heavy-tailed distribution-score is a statistical measure that tells you how far a data point is from the rest of the dataset. In a more technical term, Z-score tells how many standard deviations away a given observation is from the mean.![download (18)](https://user-images.githubusercontent.com/112580968/205923511-414c3f0b-8c5f-44ab-9b15-2e93744f41db.png)


Feature Scaling:

Feature Scaling is a technique to standardize the independent features present in the data in a fixed range. It is done to prevent biased nature of machine learning algorithms towards features with greater values and scale. The two techniques are:

Normalization: is a scaling technique in which values are shifted and rescaled so that they end up ranging between 0 and 1. It is also known as Min-Max scaling. [0,1]

Standardization: is another scaling technique where the values are centred around the mean with a unit standard deviation. This means that the mean of the attribute becomes zero and the resultant distribution has a unit standard deviation. [-1,1] .

Normalization of the continuous variables was done further.

One hot encoding:
For categorical variables where no such ordinal relationship exists, the integer encoding is not enough. We have categorical data integers encoded with us, but assuming a natural order and allowing this data to the model may result in poor performance.
Many of the features such as DayofWeek, Store Type and Assortments were categorical in nature and had to be one hot encoded to continue.

Baseline Model - Decision Tree:
A baseline is a simple model that provides reasonable results on a task and does not require much expertise and time to build. It is well established that there is seasonality involved and no linear relationship is possible to fit. For these kinds of datasets tree-based machine learning algorithms are used which are robust to outlier effects which can handle non-linear data sets effectively.
Decision Tree is a Supervised learning technique that can be used for both Classification and Regression problems. It is a tree-structured classifier, where internal nodes represent the features of a dataset, branches represent the decision rules, and each leaf node represents the outcome.![download (19)](https://user-images.githubusercontent.com/112580968/205923751-0d26ea6d-b240-4009-b7ef-4652ef90d364.png)


Conclusion and Recommendations:
Conclusion:
The main objective of sales forecasting is to paint an accurate picture of expected sales. Sales teams aim to either hit their expected target or exceed it.
When the sales forecast is accurate, operations go smoothly and future planning for the company's growth is done efficiently.
Upon having this analysis, it can be established that given the dataset, the model developed is able to explain 95.5878 % of the variations and is able to predict the sales values in a good range.
Some important insights to draw from the analysis includes:
•	There were more sales on Monday. probably because shops generally remain closed on Sundays which had the lowest sales in a week. This validates the hypothesis about this feature.
•	The positive effect of promotion on Customers and Sales is observable. Most stores have competition distance within the range of 0 to 10 kms and had more sales than stores far away, probably indicating competition in busy locations ? vs remote locations.
•	Store type B though being few in number had the highest sales average. The reasons include all three kinds of assortments specially assortment level b which is only available at type b stores and being open on Sundays as well. The outliers in the dataset showed justifiable behaviour. The outliers were either of store type b or had promotion going on which increased sales.

Recommendations:
•	More stores should be encouraged for promotion. 
•	Store type B should be increased in number.
•	There's a seasonality involved; hence the stores should be encouraged to promote and take advantage of the holidays.








