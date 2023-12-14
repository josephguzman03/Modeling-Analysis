# Modeling Analysis based on Calorical Values 

Welcome to our Data Science 80 (DSC80) project at UC San Diego, where we embark on a flavorful journey through the realms of predictive modeling and fairness analysis. Our goal for this project is centered around predicting the average rating of recipes and unraveling the subtle interplay between caloric content, the number of ingredients, and the culinary alchemy that defines each dish. This research takes a deeper look at our previously conducted project, "Significant Relations with Ratings of Recipes." It unfolds across four distinct sections: *Framing the Problem*, *Baseline Model*, *Final Model*, and *Fairness Analysis*.

Writen by Aryan Shah & Joseph Guzman


---

# Framing the Problem

In this project, our goal is to predict the **average rating of a recipe** based on two key features: *caloric content* and *number of ingredients*. This task falls under the realm of regression, given that our response variable, `average_rating`, is continuous.

**Response Variable:** Our focus is on the `average_rating` variable, chosen as the target outcome for prediction. The aim is to discern how the caloric content and the number of ingredients influence a recipe's average rating.

**Evaluation Metric:** To gauge the model's performance, we use *Root Mean Squared Error (RMSE)*. This metric suits regression problems, providing an average measure of prediction error magnitude. RMSE is calculated as the square root of the average squared differences between predictions and actual observations. It was preferred over alternatives like Mean Absolute Error (MAE) due to its emphasis on larger errors.

**Features Known at Time of Prediction:** During prediction, we have information about the caloric content and the number of ingredients, as these metrics are typically derived from the recipe's ingredients and quantities. Consequently, our model can be trained using these features.


| name                                 |     id |   minutes |   contributor_id |   n_steps |   n_ingredients |   average_rating |   calories |
|:-------------------------------------|-------:|----------:|-----------------:|----------:|----------------:|-----------------:|-----------:|
| 1 brownies in the world    best ever | 333281 |        40 |           985201 |        10 |               9 |                4 |      138.4 |
| 1 in canada chocolate chip cookies   | 453467 |        45 |          1848091 |        12 |              11 |                5 |      595.1 |
| 412 broccoli casserole               | 306168 |        40 |            50969 |         6 |               9 |                5 |      194.8 |
| millionaire pound cake               | 286009 |       120 |           461724 |         7 |               7 |                5 |      878.3 |
| 2000 meatloaf                        | 475785 |        90 |          2202916 |        17 |              13 |                5 |      267   |


---

# Baseline Model

## Modeling Features

For this task, we employed a straightforward **Linear Regression** model. Linear Regression is a basic and widely used form of predictive analysis, operating on the assumption of linearity between dependent and independent variables.

The model incorporates the following features:

- **`calories`:** This is a quantitative feature that signifies the caloric content of a recipe. It is treated as a continuous variable.
- **`n_ingredients`:** Another quantitative feature, this represents the count of ingredients in a recipe. It is considered a discrete variable.

Both features are numerical, eliminating the presence of ordinal or nominal features in the model. As a result, encoding was unnecessary.


## Model's Performance

The performance of the model was evaluated using the *Root Mean Squared Error (RMSE)* metric. The RMSE value represents the standard deviation of the residuals (prediction errors). Lower values of RMSE indicate better fit.

Whether the model is "good" or not depends on the specific RMSE value obtained. Generally, a lower RMSE value indicates a better fitting model. However, it's also important to compare this baseline model's performance with other more complex models to truly assess its goodness.

The **RMSE** value of 0.6422392472136152 indicates the average magnitude of prediction errors. In the context of predicting average ratings (usually between 1 and 5), an RMSE of 0.642 suggests that, on average, the model's predictions deviate by approximately 0.642 from the true values.

The **RMSE** value of approximately 0.6422 should be interpreted in the context of the target variable (average_rating), which typically ranges between 1 and 5. This level of error may be considered reasonable**.

It's worth noting that opting for a simpler model with a slightly higher RMSE could be preferred over a complex model with a slightly lower RMSE, considering the trade-off between bias and variance (overfitting).


---

# Final Model

## Modeling Features

In our final model, we utilized three features for the prediction task: `calories`, `n_ingredients`, and `n_steps`. These features were selected based on their relevance to the culinary context and their potential impact on a recipe's average rating:

- **`calories`:** This quantitative feature, similar to our baseline model, represents the caloric content of a recipe. It remains a continuous variable. Notably, it helps capture variations in data points based on the external biases of higher or lower-calorie meals.

- **`n_ingredients`:** Also a quantitative feature, this represents the count of ingredients in a recipe, much like in our baseline model. It is a discrete variable, and a higher number of ingredients may influence the average rating.

- **`n_steps`:** A novel addition to our model, this feature refines our predictive values by representing the number of steps required to complete a recipe. The concept suggests that more steps might lead to a "prestige" result.

We maintained a numerical feature approach similar to our baseline model, eliminating the need for encoding due to the absence of ordinal or nominal features. While considering features like `minutes` initially, we prioritized runtime efficiency and settled on `calories`, `n_ingredients`, and `n_steps` as more suitable.

The chosen modeling algorithm is a **Random Forest Regressor**, an ensemble learning method that combines multiple decision trees to enhance predictive performance and control overfitting.

The hyperparameters employed in our model include:

- **n_estimators:** The number of trees in the forest.
- **max_depth:** The maximum depth of the trees.

The method for the Hyperparameter Selection:

We utilized the **GridSearchCV** method for hyperparameter selection. This approach thoroughly explores a predefined hyperparameter grid, employing cross-validation to assess each combination's performance. The combination yielding the best results, measured by negative mean squared error, on the training set is chosen.

## Model's Peformance

In evaluating the Final Model, we considered the Root Mean Squared Error (RMSE) as well. The Baseline Model, utilizing Linear Regression, produced an RMSE of approximately 0.6422. Meanwhile, the Final Model, employing a Random Forest Regressor with optimized hyperparameters through GridSearchCV, achieved an RMSE of 0.6423142219305189.

Comparing these RMSE values, we note a slight increase in the Final Model's RMSE compared to the Baseline Model. It's crucial to interpret this result within the context of the prediction task and the data's characteristics. While a lower RMSE generally indicates improved predictive accuracy, the marginal difference suggests that the Random Forest model, despite its complexity, doesn't notably outperform the simplicity of the Linear Regression baseline in this scenario.

As mentioned earlier, the choice between a simpler model with slightly higher RMSE and a more complex model with slightly lower RMSE involves a trade-off between bias and variance. The final model's performance should be considered within this trade-off, ensuring it not only enhances predictive accuracy but also generalizes effectively to new data and aligns with the predictive modeling task's objectives.

---

# Fairness Analysis 

## Hypothesis Analysis

During our data review, we were keen on understanding how our final models might be influenced by specific quantitative features. We honed in on exploring the fairness related to the number of ingredients, specifically those with fewer than 10. Our goal was to uncover any potential biases in the model predictions.

**Null Hypothesis (H0)**: Our model is fair. The RMSE-based average rating prediction performance does not significantly differ between recipes with fewer than 10 ingredients (Group X) and those with 10 or more ingredients (Group Y). Any observed differences are likely due to chance.

**Alternative Hypothesis (H1)**: Our model is not fair. The RMSE-based average rating prediction performance significantly differs between recipes with fewer than 10 ingredients (Group X) and those with 10 or more ingredients (Group Y). This suggests that the model's accuracy varies across these groups.

*Group X*: Recipes with a number of ingredients less than 10.
*Group Y*: Recipes with a number of ingredients greater than or equal to 10.

For the **Evaluation Metric**, we decided to continue using Root Mean Squared Error (RMSE).

In terms of the **Test Statistic**, we conducted Permutation tests based on the absolute difference in RMSE between Group X and Group Y.
 
The chosen **Significance Level (α)** for our analysis is 0.05.


## Permutation Testing 

<iframe src="assets/Permutation_Test.html" width=800 height=600 frameBorder=0></iframe>

The resulting p-value came out to be 0.888. With a p-value greater than the significance level of 0.05, specifically 0.888, we **fail to reject** the null hypothesis. This means there isn't sufficient evidence to conclude a significant difference in the average rating prediction performance between recipes with fewer than 10 ingredients and recipes with 10 or more ingredients.

## Conclusion

In conclusion, we built a unified predictive model using a **Random Forest Regressor** enhanced by a *linear regressor model*. It's crucial to understand that our model doesn't offer absolute certainty, as conclusive assertions can't be made with 100% certainty. The results from our fairness analysis indicate that the selected model aligns with fairness considerations in the given data. As we navigate this concept, we recognize the nuanced nature of statistical testing and emphasize that our conclusions are made within the bounds of our data, methodology, and inherent uncertainties associated with observational analyses.
