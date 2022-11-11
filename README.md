# Terry-Stops-Classification

## Creating a Classification model to predict Arrests

The stakeholder of this assignment is Campaign Zero, a national organization devoted to lobbying legislators on ten policy solutions that reduce police violence, including independent oversight, legal bans on the use of force, and the end of for-profit policing. Campaign Zero tasked us with researching Terry Stop data using the Seattle PD data as a sample. Campaign Zero wants to use this data to determine some of the best predictors of arrests.

Note about feature elimination - One column titled 'Arrest Flag' seemed to be too closely related to the target variable. I ran the final model with and without this column to see the results. These results will be discussed later and the impact on future recommendations.

## Step 1 - Data Preparation and Feature Engineering

A large amount of time was placed into setting up the data to be modeled. While the feature responses were mostly uniform, there were multiple errors within each feature that would've created unnecessary noise when modeling. Once all the features were cleaned I went forward with engineering 3 new features in order to get the most out of mostly unusable old ones. Two features, Time Reported and Day Reported were used to create 3 new features. A Day/Night feature which told me at what time the call was reported, and a Month feature, telling me which month the call was reported, and a Week feature, which told me which week in the month a call was reported. I thought these might be useful because crimes might be more or less likely to occur during certain months, weeks, or times of the day.

## Step 2 - Baseline Model

For the baseline model I used a Logistic Regression model. I wanted to use something simple and quick to train in order to see how it would do. This model had an average validation score of .75, which is not very notable because the data is split with 75% 'No Arrest', 25% 'Arrest'. But a baseline that is guessing the larger proportion would make sense.

## Step 3 - Model Iteration

Next I focused on more advanced models and using GridSearchCV to find the best hyperparameters in order to obtain the best scores. The first model I tried here was a perceptron. It only performed at 73% so rather than spending more time I moved on. I then trained a decision tree which got a 69% validation score. While this was much lower, I knew the grid search would help, and the model then obtained a 75% training score and a 76% test score. The final model was the XGBoost model. The initial version had a train score of 80% and a test score of 76%. 

Important note regarding model metrics - A classification report was printed after every model and the precision score did not exceed 80% for the No Arrest target, which means none of the models were purely guessing No Arrest over actually learning something from the data. 

## Step 4 - Best Model and Feature Importance

The XGBoost model performed the best and I used this model to obtain the feature importance and learn about what it used as weights for the features. Precinct was overwhelmingly the best predictor for this model, followed by Beat and Sector. Intuitively, this makes sense, location is important. Neighborhoods are often policed differently, but from this data alone, no further conclusions can be drawn.

<img width="987" alt="Screen Shot 2022-11-11 at 5 31 26 PM" src="https://user-images.githubusercontent.com/104473048/201439833-9499273e-9ff5-4862-8ea5-ef6994c40d8e.png">

<img width="390" alt="Screen Shot 2022-11-11 at 5 33 47 PM" src="https://user-images.githubusercontent.com/104473048/201439930-9397fae4-78c5-4bb0-b266-dab5de41d87c.png">

## Notes about 'Arrest Flag' feature

When this feature was added, the best model actually obtained an 86% train score, and an 80% test score. The feature was the number one most important feature with nearly a .5 weight for importance. If the goal in the future is to strictly predict if an arrest was made, adding this feature would be beneficial to all future modeling. However, due to the overlap between this feature and the target, including it pushes other important features further down the list, and may make it harder to draw better conclusions. Use this feature appropriately in the future.

<img width="971" alt="Screen Shot 2022-11-11 at 5 42 38 PM" src="https://user-images.githubusercontent.com/104473048/201440637-2923932e-0d68-49c7-95e1-2f14b6b2d4a5.png">

## Recommendations

Like I mentioned above, location is a key feature and should be further explored. Obtaining socioeconomic data in the form of a census, with features like income, population, population by race. Historically these features paint a better picture about policing in different neighborhoods. Having that data here would be insightful, but without it, no further conclusions can be drawn.

## Repository Structure

```
├── data
├──.gitignore
├── Project 2 presentation.pdf
├── README.md
├── student.ipynd
└── student.pdf
