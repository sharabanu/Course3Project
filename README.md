# Course 
Getting and Cleaning Data

## Project Assignment
The purpose of this project is to demonstrate your ability to collect, work with, and clean a data set. The goal is to prepare tidy data that can be used for later analysis.

## Introduction
Previously limited to the largest of large companies processing massive quantities of data with internally purpose-built engines, today’s sophisticated data collection and analysis is democratized through open source data stacks that continue to drive the costs of insights and predictive modeling down. When combined with the enormous amount of data driven from social, mobile, and sensor-driven applications, this new competency in big data is changing the expectations for what is possible at the application level. For example companies like Fitbit, Nike, and Jawbone Up are racing to develop the most advanced algorithms to attract new users. 

In this assignment the data that will be used is in the course website which represent data collected from the accelerometers from the Samsung Galaxy S smartphone:

Here are the data for the project:

https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip


A full description is available at the site where the data was obtained:

http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones 

##For this assignment I have create one R script called run_analysis.R which performed the following tasked: 

##1)  Merges the training and the test sets to create one data set.
      subject <- rbind(subjectTrain, subjectTest)
      activity <- rbind(activityTrain, activityTest)
      features <- rbind(featuresTrain, featuresTest)

      -Name the column names from the features file in variable featureNames
      colnames(features) <- t(featureNames[2])

      -Add activity and subject as a column to features
        colnames(activity) <- "Activity"
        colnames(subject) <- "Subject"
        completeData <- cbind(features,activity,subject)
        
##2)Extracts only the measurements on the mean and standard deviation for each measurement. 
    -Adding activity and subject columns
    requiredColumns <- c(columnsWithMeanSTD, 562, 563)

    -Look at the number of variables in completeData
    dim(completeData)
    extractedData <- completeData[,requiredColumns]

    -Look at the number of variables in extractedData
    dim(extractedData)
 
##3)Uses descriptive activity names to name the activities in the data set
    extractedData$Activity <- as.character(extractedData$Activity)
    for (i in 1:6)
    {
      extractedData$Activity[extractedData$Activity == i] <- as.character(activityLabels[i,2])
    }
    
    -Set the activity variable in the data as a factor
    extractedData$Activity <- as.factor(extractedData$Activity)

##4)Appropriately labels the data set with descriptive variable names. 

--Look at variable names
names(extractedData)

--Acc can be replaced with Accelerometer
--Gyro can be replaced with Gyroscope
--BodyBody can be replaced with Body
--Mag can be replaced with Magnitude
--Character 'f' can be replaced with Frequency
--Character 't' can be replaced with Time

names(extractedData)<-gsub("Acc", "Accelerometer", names(extractedData))
names(extractedData)<-gsub("Gyro", "Gyroscope", names(extractedData))
names(extractedData)<-gsub("BodyBody", "Body", names(extractedData))
names(extractedData)<-gsub("Mag", "Magnitude", names(extractedData))
names(extractedData)<-gsub("^t", "Time", names(extractedData))
names(extractedData)<-gsub("^f", "Frequency", names(extractedData))
names(extractedData)<-gsub("tBody", "TimeBody", names(extractedData))
names(extractedData)<-gsub("-mean()", "Mean", names(extractedData), ignore.case = TRUE)
names(extractedData)<-gsub("-std()", "STD", names(extractedData), ignore.case = TRUE)
names(extractedData)<-gsub("-freq()", "Frequency", names(extractedData), ignore.case = TRUE)
names(extractedData)<-gsub("angle", "Angle", names(extractedData))
names(extractedData)<-gsub("gravity", "Gravity", names(extractedData))

##5)From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

extractedData$Subject <- as.factor(extractedData$Subject)
extractedData <- data.table(extractedData)

-Create tidyData as a set with average for each activity and subject
TidyData <- aggregate(. ~Subject + Activity, extractedData, mean)

-Order tidayData according to subject and activity
TidyData <- TidyData[order(TidyData$Subject,TidyData$Activity),]

-Write tidyData into a text file named TidyData.txt
write.table(TidyData, file = "TidyData.txt", row.names = FALSE)

#End 
