# 21 th solution for Predict Student Performance from Game Play

Firstly, I extend my gratitude to the Kaggle community for its invaluable discussions, the hosts for organizing this engaging competition.

## Competition Overview:
My approach to the competition was methodical, focusing on robust feature engineering and ensemble modeling. I didn't rely on any extraordinary methods; instead, I emphasized iterative improvements and strategic model combinations.

## Models and Ensemble Strategy:
I deployed an ensemble of LightGBM, Neural Networks (NN), and XGBoost models, with additional use of Catboost, MLP, and Logistic Regression in various stages. The NN models combined Transformer and GRU layers, with standalone Transformers underperforming on their own. For LightGBM, separate models were trained for different level groups, with a distinction made for level groups 13-22, where each target had its own model.

## Features:
Feature set was expansive and dynamic, with the number of features increasing per level group:

- Level group 0-4: 3009 features
- Level group 5-12: 9747 features
- Level group 13-22: 18610 features
=> Features included statistical measures of numerical data, elapsed times between key in-game events, counts of categorical data, and the usage of previous level group features as well as predicted probabilities for the current level group. Notably, the 'Checkpoint feature'—the time taken between significant in-game events—proved highly impactful.

## Cross-Validation and Training:
I utilized nested cross-validation, with a preference for 10-fold over 5-fold as it yielded marginally higher CV scores. Stratified K-fold strategy was aligned with the distribution of the total number of correct answers by the users. The models were trained on the training data (session_id starting with 2200 or less) and validated on the validation data (session_id starting with 2201 or more). For feature selection, we used the top 500 features based on their importance, carefully avoiding data leakage.

## Results:
My models achieved the following scores:
- LightGBM CV: 0.7032, Public Score: 0.704, Private Score: 0.701
- NN CV: 0.7010, Public Score: 0.700, Private Score: 0.700
- Ensemble CV: 0.7053, Public Score: 0.706

The final merged submission (averaging LightGBM and Catboost) had a CV of 0.7024, with Public and Private Leaderboard scores at 0.7 and 0.702, respectively.
Inference Times and Optimizations:
Inference times varied across models, with LightGBM taking 90 minutes, Catboost 120 minutes, and the merged approach 150 minutes. Significant speed improvements were noted by using the 'lleaves' library for compiling the LightGBM model.

## Final Notes:
Threshold optimization and feature engineering were the cornerstones of my success, while the use of LSTM and CNN models did not contribute positively to the CV scores. The efforts in ensemble, threshold optimization, and careful feature selection were pivotal in securing my place.

For further details and insight into my methods, my inference code is shared on Kaggle and GitHub.