# Modeling-Analysis based on Calorical Values 

Welcome to our Data Science 80 (DSC80) project at UC San Diego, where we delve into the captivating realm of culinary exploration. Our project centers around unraveling the intricate relationship between the caloric content of recipes and their corresponding average ratings. This research is a continuous of our previous project, "Significant relations with ratings of recipes". This research unfolds across four distinct sections: *Framing the Problem*, *Baseline Model*, *Final Model* and *Fairness Analysis*.


Writen by Aryan Shah & Joseph Guzman


---

# Framing the Problem

The prediction problem is to predict the ***average rating of a recipe based on its caloric content and the number of ingredients***. This is a regression problem as the response variable, `average_rating`, is continuous.

**Response Variable:** The response variable is `average_rating`. This variable was chosen because it is the target outcome that we want to predict. The goal is to understand how the caloric content and the number of ingredients in a recipe influence its average rating.

**Evaluation Metric:** The metric used to evaluate the model is *Root Mean Squared Error (RMSE)*. RMSE is a suitable metric for regression problems as it measures the average magnitude of the error. It's the square root of the average of squared differences between prediction and actual observation. It was chosen over other metrics like Mean Absolute Error (MAE) because it penalizes large errors more due to the squaring of the differences.

**Features Known at Time of Prediction:** At the time of prediction, we would know the caloric content of a recipe and the number of ingredients, as these are typically calculated based on the ingredients and quantities used. Therefore, we can train our model using these features.



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

The model used for this task is a simple **Linear Regression** model. Linear Regression is a basic and commonly used type of predictive analysis which usually works on the principle of linearity between dependent and independent variables.

The features used in the model are:

`calories` - This is a quantitative feature representing the caloric content of a recipe. It is a continuous variable.
`n_ingredients` - This is also a quantitative feature representing the number of ingredients in a recipe. It is a discrete variable.
Both of these features are numerical, so there are no ordinal or nominal features in this model. Therefore, no encoding was necessary.

## Model's Performance

The performance of the model was evaluated using the *Root Mean Squared Error (RMSE)* metric. The RMSE value represents the standard deviation of the residuals (prediction errors). Lower values of RMSE indicate better fit.

Whether the model is "good" or not depends on the specific RMSE value obtained. Generally, a lower RMSE value indicates a better fitting model. However, it's also important to compare this baseline model's performance with other more complex models to truly assess its goodness.

The RMSE value of 0.6422392472136152 indicates the average magnitude of the errors in the predictions. In the context of the average rating prediction problem, where ratings typically range between 1 and 5, an RMSE of 0.642 suggests that, on average, the model's predictions deviate by approximately 0.642 from the true values.

The RMSE value of approximately 0.6422 should be interpreted in the context of the target variable (average_rating), which typically ranges between 1 and 5. This level of error may be considered reasonable.


Remember, a simpler model with a slightly higher RMSE might be preferred over a complex model with a slightly lower RMSE due to the trade-off between bias and variance (overfitting).


---

# Final Model

## Modeling Features

In our final model, the features used for the prediction task are `calories`, `n_ingredients`, and `n_steps`. These features were chosen based on their relevance to the culinary context and their potential influence on the average rating of a recipe:

Calories (`calories`): The caloric content of a recipe is a crucial factor as it directly relates to the nutritional aspect of the dish. Different individuals might have preferences for higher or lower-calorie meals, and this feature can capture those variations in taste.
Number of Ingredients (`n_ingredients`): The complexity and diversity of a recipe can be reflected in the number of ingredients. More ingredients might contribute to a richer and potentially more flavorful dish, influencing the average rating.
Number of Steps (`n_steps`): The number of steps in a recipe could indicate the level of intricacy or difficulty involved in preparing the dish. This complexity might affect the overall satisfaction of individuals preparing the recipe, thus impacting the average rating.

Including these features is grounded in the assumption that factors like taste, complexity, and nutritional content play a role in determining how a recipe is rated.

The chosen modeling algorithm is a **Random Forest Regressor**. Random Forest is an ensemble learning method that combines multiple decision trees to improve predictive performance and control overfitting.

Hyperparameters used on our model:

**n_estimators**: The number of trees in the forest.
**max_depth**: The maximum depth of the trees.

Method for our Hyperparameter Selection:

**GridSearchCV**: This method exhaustively searches through a specified hyperparameter grid, using cross-validation to evaluate each combination of hyperparameters. The combination that results in the best performance (in terms of negative mean squared error) on the training set is chosen.

## Model's Peformance

To evaluate the Final Model's performance, the Root Mean Squared Error (RMSE) is used. The Baseline Model, which employed Linear Regression, had an RMSE of approximately 0.6422. The Final Model's RMSE, achieved using a Random Forest Regressor and optimized hyperparameters through GridSearchCV, is 0.6423142219305189.

Comparing these RMSE values, we observe a slight increase in the RMSE for the Final Model compared to the Baseline Model. It's important to interpret this result considering the nature of the prediction task and the specific characteristics of the data. While a lower RMSE generally indicates better predictive accuracy, the small difference between the Baseline and Final Model's RMSE may suggest that the Random Forest model, despite its complexity, doesn't significantly outperform the simplicity of the Linear Regression baseline in this context.

As mentioned earlier, the choice between a simpler model with slightly higher RMSE and a more complex model with slightly lower RMSE involves a trade-off between bias and variance. The final model's performance should be considered in the context of this trade-off, ensuring that it not only improves predictive accuracy but also generalizes well to new data and aligns with the goals of the predictive modeling task.

---

# Fairness Analysis 

## Hypothesis Analysis

When we looked over the data, we were interested in which feature would be affected more. We decided to dive into the fairness of the number of ingredients less than 10, and see if there is any affects when using our final models. 

**Null Hypothesis (H0)**: Our model is fair. The average rating prediction performance, as measured by RMSE, does not significantly differ between recipes with fewer than 10 ingredients (Group X) and recipes with 10 or more ingredients (Group Y). Any observed differences are likely due to chance.

**Alternative Hypothesis (H1)**: Our model is not fair. The average rating prediction performance, as measured by RMSE, significantly differs between recipes with fewer than 10 ingredients (Group X) and recipes with 10 or more ingredients (Group Y). There is evidence that the model's accuracy is not consistent across these groups.

*Group X*: Recipes with a number of ingredients less than 10.
*Group Y*: Recipes with a number of ingredients greater than or equal to 10.

For our Evaluation Metric, we decided to continue using Root Mean Squared Error (RMSE).

For our ***Test Stastic***, we conducted Permutation tests based on the absolute difference in RMSE between Group X and Group Y. We decided to use ***Significance Level (α)***: 0.05.

## Permutation Testing 

<iframe src="assets/Permutation_Test.html" width=800 height=600 frameBorder=0></iframe>

The resulting p-value came out to be 0.888. With a p-value of 0.888, which is greater than the significance level of 0.05, we fail to reject the null hypothesis. There is not enough evidence to conclude that there is a significant difference in the average rating prediction performance between recipes with fewer than 10 ingredients and recipes with 10 or more ingredients.

The resulting p-value came out to be 0.888. With a p-value of 0.888, which is greater than the significance level of 0.05, we fail to reject the null hypothesis. There is not enough evidence to conclude that there is a significant difference in the average rating prediction performance between recipes with fewer than 10 ingredients and recipes with 10 or more ingredients.


---

## Conclusion

In conclusion, our culinary data science exploration provides insights into the delicate balance between model complexity, predictive accuracy, and fairness. As we navigate this realm, we acknowledge the nuanced nature of statistical testing and emphasize that our conclusions are drawn within the bounds of our data, methodology, and inherent uncertainties associated with observational analyses.