## Code book for Assignment Module 3
#Getting and Cleaning Data Course Project - CodeBook

#Description

Additional information about the variables, data and transformations used in the course project for the Getting and Cleaning Data course.

#Dataset
The data linked to from the course website represent data collected from the accelerometers from the Samsung Galaxy S smartphone. A full description is available at the site where the data was obtained:

http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

The data can be downloaded from https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

#Input from Data Set

The input data containts the following data files:

* X_train.txt contains variable features that are intended for training.
* y_train.txt contains the activities corresponding to X_train.txt.
* subject_train.txt contains information on the subjects from whom data is collected.
* X_test.txt contains variable features that are intended for testing.
* y_test.txt contains the activities corresponding to X_test.txt.
* subject_test.txt contains information on the subjects from whom data is collected.
* activity_labels.txt contains metadata on the different types of activities.
* features.txt contains the name of the features in the data sets.

#Transformations of the Data set

* X_train.txt is read into featuresTrain.
* y_train.txt is read into activityTrain.
* subject_train.txt is read into subjectTrain.
* X_test.txt is read into featuresTest.
* y_test.txt is read into activityTest.
* subject_test.txt is read into subjectTest.
* features.txt is read into featureNames.
* activity_labels.txt is read into activityLabels.
* The subjects in training and test set data are merged to form subject.
* The activities in training and test set data are merged to form activity.
* The features of test and training are merged to form features.
* The name of the features are set in features from featureNames.
* features, activity and subject are merged to form completeData.
* Indices of columns that contain std or mean, activity and subject are taken into requiredColumns .
* extractedData is created with data from columns in requiredColumns.
* Activity column in extractedData is updated with descriptive names of activities taken from activityLabels. Activity column is expressed as a factor variable.
* Acronyms in variable names in extractedData, like 'Acc', 'Gyro', 'Mag', 't' and 'f' are replaced with descriptive labels such as 'Accelerometer', 'Gyroscpoe', 'Magnitude', 'Time' and 'Frequency'.
* tidyData is created as a set with average for each activity and subject of extractedData. Entries in TidyData are ordered based on activity and subject.
* Finally, the data in TidyData is written into TidyData.txt.

#Output
TidyData.txt contains the clean and tidy data that was processed. The header line contains the names of the variables. It contains the mean and standard deviation values of the data contained in the input files. The header is restructued in an understandable manner.
