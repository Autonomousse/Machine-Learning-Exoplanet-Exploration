# Machine-Learning-Exoplanet-Exploration

## Background:

Over a period of nine years in deep space, the NASA Kepler space telescope has been out on a planet-hunting mission to discover hidden planets outside of our solar system.
To help process this data, you will create machine learning models capable of classifying candidate exoplanets from the raw dataset.

## Procedure:

### Preprocess the Data
* Preprocess the dataset prior to fitting the model.
* Perform feature selection and remove unnecessary features.
* Use MinMaxScaler/StandardScaler to scale the numerical data.
* Separate the data into training and testing data.

### Tune Model Parameters
* Use GridSearch to tune model parameters.
* Tune and compare at least two different classifiers.

### Reporting
* Compare each model's performance as well as a summary about your findings and any assumptions you can make based on your model (is your model good enough to predict new exoplanets? Why or why not? What would make your model be better at predicting new exoplanets?).

### Note
* sklearn upgrade and install joblib will need to be uncommented prior to first run to make sure everthing is up to date.

## Report:

The first machine learning model used was Random Forest. Prior to running the training and testing data, `koi_disposition` was chosen to be the target value (y). For the features (x), all of the uncertainties were dropped (all of the columns that ended with `err01` and `err02`) under the assumption that these features may not actually be very useful for the model. Next, train test split and a label encoder were utilized to map the target into numerical placeholders. Preprocessing involved scaling the testing and training data with the MinMaxScaler and then using RandomForestClassifier to train the model. Initially receiving a training score of 1.00 and a testing score of 0.895, which means that the model is doing a good job of making predictions. However we still have a lot of features and the model may be overfitting. Run the same procedure without removing any features and the training score is again 1.00 and the testing score is 0.896. This is very similar and allows for a reduction of features. Using feature importance to create a list of features in descending order based on significance, select the top 6 features and rerun the same training and testing procedure once more. This time the training score is 0.999 and the testing score is 0.863. Still extremely close to the original scores received and allowing for hyperparameter tuning. GridSearchCV with 5 folds and 16 candidates (4x4 matrix of n_estimators and max_depths) totals 80 fits. The best fit brought the training score down to 0.903 but brough the testing score up to 0.886 so the model has some improvement.

For the SVM model, the same process was used as for the Random Forest model. The main differnce here was that the feature selection was done from the Random Forest feature importance. The lowest 6 features were dropped and everything else was kept in the data. The test accuracy for this model was initially 0.883 and rose slightly after tuning the hyperparameters to 0.884. The classification report indicates that this model would be good for predicting false positive exoplanets (0.97 precision) but not as good for predicting candidates planets (0.77 precision)
