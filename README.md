# Terry-Stops-Classification

## Creating a Classification model to predict Arrests

The stakeholder of this assignment is Campaign Zero, a national organization devoted to lobbying legislators on ten policy solutions that reduce police violence, including independent oversight, legal bans on the use of force, and the end of for-profit policing. Campaign Zero tasked us with researching Terry Stop data using the Seattle PD data as a sample. Campaign Zero wants to use this data to determine some of the best predictors of arrests.

Note about feature elimination - One column titled 'Arrest Flag' seemed to be too closely related to the target variable. I ran the final model with and without this column to see the results. These results will be discussed later and the impact on future reccomendations.

## Step 1 - Data Preperation and Feature Engineering

A large amount of time was placed into setting up the data to be modeled. While the feature responses were mostly uniform, there were multiple errors within each feature that would've created unnecisary noise when modeling. Once all the features were cleaned I went forward with engineering 3 new features in order to get the most out of mostly unusable old ones. Two features, Time Reported and Day Reported were used to create 3 new features. A Day/Night feature which told me at what time the call was reported, and a Month feature, telling me which month the call was reported, and a Week feature, which told me which week in the month a call was reported. I thought these might be useful because crimes might be more or less likely to occur during certain months, weeks, or times of the day.

## Step 2 - Baseline Model

For the baseline model I used a Logistic Regression model. I wanted to use something simple and quick to train in order to see how it would do. This model had an average validation score of .75, which is not very notable because the data is split with 75% 'No Arrest', 25% 'Arrest'. But a baseline that is guessing the larger proportion would make sense.

## Step 3 - Model Iteration

Next I focused on more advanced models and using GridSearchCV to find the best hyperparameters in order to obtain the best scores. The first model I tried here was a perceptron. It only performed at 73% so rather than spending more time I moved on. I then trained a decision tree which got a 69% validation score. While this was much lower, I know the grid search would help, and the model then obtained a 75% training score and a 76% test score. The final model was XGBoost model. The initial version had a train score of 80% and a test score of 76%. 

# Step 4 - Best Model and Feature Importance

The XGBoost model performed the best and I used this model to obtain the feature importance and learn about what it used as weights for the features. 

├── data
├──.gitignore
├── Terry Stops Presentation.pdf
├── README.md
├── student.ipynd
└── student.pdf
