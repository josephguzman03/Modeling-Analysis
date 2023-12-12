# Modeling-Analysis based on Calorical Values 

Welcome to our Data Science 80 (DSC80) project at UC San Diego, where we delve into the captivating realm of culinary exploration. Our project centers around unraveling the intricate relationship between the caloric content of recipes and their corresponding average ratings. This research is a continuous of our previous project, "Significant relations with ratings of recipes". This research unfolds across four distinct sections: *Framing the Problem*, *Baseline Model*, *Final Model* and *Fairness Analysis*.


Writen by Aryan Shah & Joseph Guzman


---

## Framing the Problem

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

## Baseline Model

The model used for this task is a simple **Linear Regression** model. Linear Regression is a basic and commonly used type of predictive analysis which usually works on the principle of linearity between dependent and independent variables.

The features used in the model are:

`calories` - This is a quantitative feature representing the caloric content of a recipe. It is a continuous variable.
`n_ingredients` - This is also a quantitative feature representing the number of ingredients in a recipe. It is a discrete variable.
Both of these features are numerical, so there are no ordinal or nominal features in this model. Therefore, no encoding was necessary.

The performance of the model was evaluated using the *Root Mean Squared Error (RMSE)* metric. The RMSE value represents the standard deviation of the residuals (prediction errors). Lower values of RMSE indicate better fit.

Whether the model is "good" or not depends on the specific RMSE value obtained. Generally, a lower RMSE value indicates a better fitting model. However, it's also important to compare this baseline model's performance with other more complex models to truly assess its goodness.

The RMSE value of 0.6422392472136152 indicates the average magnitude of the errors in the predictions. In the context of the average rating prediction problem, where ratings typically range between 1 and 5, an RMSE of 0.642 suggests that, on average, the model's predictions deviate by approximately 0.642 from the true values.

The RMSE value of approximately 0.6422 should be interpreted in the context of the target variable (average_rating), which typically ranges between 1 and 5. This level of error may be considered reasonable.


Remember, a simpler model with a slightly higher RMSE might be preferred over a complex model with a slightly lower RMSE due to the trade-off between bias and variance (overfitting).


---

## Final Model

---

## Fairness Analysis 

---

## Conclusion