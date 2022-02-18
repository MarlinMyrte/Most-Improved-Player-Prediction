# Most-Improved-Player-Prediction

## This a repo for my a project where I'm trying to predict the winner of the Most Improved Player award (MIP) in the NBA for 2022.

The MIP award is probably my favourite awards among all the other ones as it is given to the player who has put the most effort in improving his game and has reached a new level on the way he's playing. It is a reward for all the dedication and the effort that was put into training and improving. It is not only about improving your individual stats but also the impact you make on the court, how the defense perceives you and makes adjustments for you and the value you add to your team. Usually winners of the MIP go on to become All Stars and NBA Champions. This year, the top 5 candidates according to many websites are Ja Morant, Darius Garland, Miles Bridges, Desmond Bane and Dejounte Murray with Ja Morant emerging as the number 1 favorite. In many occassions narratives built around those players and hype play a big role in the process of giving out these awards. Let's see if the numbers support these candidacies and if the hype is real.  

In this project I:
- Created a pipeline to extract data from basketballreference.com using BeautifulSoup
- Cleaned the data and performed all necessary transformations
- Created plots to see some basic relationships
- Tried to predict the winner of the 2022 MIP award using 2 methods (Classification & Regression)
- Performed ensembles of the best methods to come up with predictions


## Data & Data Extraction

In order to make my prediction for the 2022 MIP award winner I used the performances of all previous winners and candidates from 1986 until 2021 (the year when the award was introduced for the first time). More specifically, I was interested in their performance during the season they won the award and the previous season and I used Basic stats as well as Advanced Stats. The candidates for each season were selected on the basis of players who received votes for the MIP award. This data was used as my training set.

*For the 1987 season, there was no voting and for that reason I decided to exclude the whole season from the project.

As for the test set, I used Basic and Advanced stats from active NBA players in the current season, excluding Rookies and players who had played less than 30 games this season or the previous one.

## Basic plots

## Data transformations

The reason why I decided to also include data from the previous season for all players is of course to calculate the difference in their performance. After all, the award is named Most Improved Player and some comparison with previous performances has to be made.

I also wanted to test whether ranked data would add more value than simple data. Therefore, I transformed each player's performance in each statistical category into a percentile rank to in which percentile each player belongs.

I also tried to scale the target variable for the regression method (check below) in order to add some "distance" between the winners of each year and the runner-ups.

Another transformation I wanted to explore was to oversample the training sample by repeating some rows of players that won the award as in some years the canidate pool was very low.

## 2 approaches

### Classification

This problem can be approached from 2 different perspectives. The first one is to try to make a prediction by using a classification model. In this case the target variable in our training set is either 1 (for winners of the award) or 0 (for the candidates that season). The Classifiers I used were:
- Logistic Regression
- K Nearest Neighbors
- Random Forest
- Xtreme Gradient Boosting

I ran these classifiers for 3 different datasets:
- Data with no transformation
- Percentile ranked data
- Oversampled data

The dataset with the percentile ranked data had the best average accuracy so I decided to use that one for the rest of the Classification approach
![alt text](https://github.com/MarlinMyrte/Most-Improved-Player-Prediction/blob/main/clf_accuracies.png "Classification Accuracies")

#### Feature selection
Afterwards, I ran an ANOVA f-test in order to find the most meaningful features in the dataset. I set an arbitrary threshold of top 10 features:
![alt text](https://github.com/MarlinMyrte/Most-Improved-Player-Prediction/blob/main/clf_best_features.png "Classification Best Features")
### Regression

We can turn this classification problem into a regression one. Instead of trying to predict the class of each player we can try to predict the votes he will get and more specifically the votes share he will get. **Add something about the voting system**. We have data for the voting results from the previous years and we will use them as our target variable. For the regression we will use the following regressors:
 - Linear Regression
 - Support Vector Regression
 - Random Forest Regressor

I ran these classifiers for 3 different datasets:
- Data with no transformation
- Percentile ranked data
- Scaled data

The dataset with the not transformed data had the best average accuracy so I decided to use that one for the rest of the Classification approach
![alt text](https://github.com/MarlinMyrte/Most-Improved-Player-Prediction/blob/main/reg_accuracies.png "Regression Accuracies")

#### Feature selection
According to Pearson's correlation the top 10 features are:
![alt text](https://github.com/MarlinMyrte/Most-Improved-Player-Prediction/blob/main/reg_best_features.png "Classification Best Features")


## Predictions

In order to make predictions I decided to use the voting ensemble method for the best models of both approaches.

### Classification
![alt text](https://github.com/MarlinMyrte/Most-Improved-Player-Prediction/blob/main/clf_pred.png "Classification Predictions")

As we can see, 3 out of the top 5 candidates appear in the prediction with Ja Morant emerging as the winner. We can also see Jordan Poole and Tyrese Maxey make an appearance. Both of them have made significant improvements in their game this season and have been getting a lot of playing time too. However, they are not the leaders on their teams or play a significant role in their team's success and that's why they might not be considered favorites by the media.

### Regression
![alt text](https://github.com/MarlinMyrte/Most-Improved-Player-Prediction/blob/main/reg_pred.png "Regression Predictions")

Once again we have Ja Morant as the winner. This time we have Dejounte Murray in the top 5 and also PJ Tucker whose stats have been improved greatly since last season as he has been getting a lot more playing time with the Heat.
