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

---

## Final Model

---

## Fairness Analysis 

---

## Conclusion