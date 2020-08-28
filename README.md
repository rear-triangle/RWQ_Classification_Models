Created by Alvaro Balkowski on August 27, 2020.

This repository is to observe the effects of multiple techniques on a single dataset, while using various classifiers. 

The classifiers used were:

- Logistic Regression
- K-Nearest Neighbors
- Kernel SVM
- Decision Tree
- Random Forest

The decision to add an ensemble method was to see whether a conventional high performing classifier would make a noticable difference to the non-ensemble methods. Other high performance methods like XGBoost could easily be added in the future, so as long as the appropriate parameter ranges are known.

Every next experiment added all techniques used in the previous experiment, as it is rare in industry not to recruit the simultaneous use of techniques to improve the performance of the classifiers used.

Experiment 1: Holdout & Scaling

A simple train/test split was used to start off, as any sensible experiment would split up training and test data at the least. The standard scaler from Sci-Kit Learn was used, which was important to standardize all features using the mean and standard deviation.

Experiment 2: Feature Selection (+ Holdout & Scaling)

The Extra Trees classifier assigns importance values to each feature and SelectFromModel picks the best ones of those. Four features were selected from eleven total features and most of those excluded features had close to zero correlation with the target variable and thus most of the noise in the dataset was excluded.

Experiment 3: Cross Validation (+ the previous two)

For this experiment and the next, the stratified k-fold cross validator was used, to account for the imbalance in the distribution of the number of examples in each class. Additionally, cross validation was performed on the training set exclusively, so as to prevent "data leakage" into the test data.

Experiment 4: Hyperparameter Tuning (+ the previous three)

Grid Search CV was used to conduct the hyperparameter tuning. Admittedly this experiment was the most computationally expensive, which is expected as not only have all of the previous techniques been used in this experiment, but grid searching is highly expensive on its own.

Results:

For every classifier with the exception of the Decision Tree classifier, the pattern was the same: high scoring in experiment 1, then progressively lower scores until Experiment 4, which reported an increase in performance. The decision tree classifier results were effectively the inverse of the rest of the classifiers. The K-Nearest Neighbors classifier had the most overall success on this dataset, with an F1 score of approximately 0.658 in the last experiment, which was the highest F1 score of any classifier or experiment. Specific results and visualizations can be seen from the RWQ_Results.xlsx file.

Challenges:


Having more data, both in number of features and number of training examples would have been an asset in improving the results from most of the experiments (naturally). The computational expense from grid searching proved too high to explore other parameters that could have yielded a better result, such as the number of estimators (trees) in the random forest parameter grid. This is possibly due to hardware limitations.

Remarks:

While a more optimal result could have been achieved by something like AutoML (or for massive datasets, cloud based pipeline architectures), my approach showcases the technical details that would be otherwise overlooked by a simple implementation of AutoML. Additionally, depending on the task, AutoML might not be the best tool to use to solve some business needs. A lot of work is still normally required to provide a clean and usable CSV file that AutoML cannot do.  

Thank you for reading!

