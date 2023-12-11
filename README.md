# Predicting Recipe Rating

Our exploratory data analysis on this dataset can be found [here](https://github.com/ShatReal/recipes-and-ratings).

## Framing the Problem

My problem is that I want to predict the rating of a recipe based on the other variables in the dataset
(minutes, date, number of steps, number of ingredients). This is a regression problem. The response
variable is rating. This is because rating is dependent on the information in the recipe, since that's
what people are judging the recipe based on. I am using the coefficient of determination to evaluate
the model because that is what the score function returns for regressors.

## Baseline Model

My model is a DecisionTreeRegressor. My model has two features: minutes,
and number of steps. They are both ordinal.

My model's score on the training data was 0.08008269158157677 and on the test data
was -0.08311626570426767, which is not very good because it is less than 0.

## Final Model

I added the features time submitted and number of ingredients, since I think that maybe
people have rated recipes differently as time goes on, and because maybe recipes with
more ingredients are rated lower because they are more complicated. I used a LinearRegression
for this model.

The model's score on the training data was 0.000951622676288788 and on the test
data was 0.0005195041382182186, which is better than the previous model because it is
greater than 0.

## Fairness Analysis

Group X is recipes that take over one hour, and Group Y is recipes that do not.
My evaluation metric is the absolute difference between the absolute differences of the
predicted rating and actual rating for both groups.

Does my model perform worse for things that take more than hour to make versus one hour or less?

Null hypothesis: The model is fair and its rmse for things that take over an hour to make and one hour or less are roughly the same, and any differences are due to random chance.

Alternative hypothesis: The model is unfair the rmse for things that take over an hour to make and one hour or less are different.

The significance level is 0.05. The p-value is 0.64. Since p > 0.05, we fail to reject the null hypothesis.