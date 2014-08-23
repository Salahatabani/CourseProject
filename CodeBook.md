This code book describes the variable in the MergedData2, which is the data set after merging train and test data
There are 88 variables, which is created after extracting the mean and standard deviation for each measurement. 
The were two types of means, the first one is direct mean (found at the end of each measurement) and the second type is found 
descripes different means. All types were extracted in this data set.
A total of 88 variables were extracted from the original data set of 563 variables.

The approach of this code bood is not to describe each and every variable in the data set, but to describe the different
measurements and how the mean is calculated for each measurement. Other than that, the variable names are self-explanatory.

"subject"
this is the subject of the experiment, there are 30 subjects in the two experiments

"activity"
The subjects performed different activities 
1 WALKING
2 WALKING_UPSTAIRS
3 WALKING_DOWNSTAIRS
4 SITTING
5 STANDING
6 LAYING

For the other 86 variables, the signals were used to estimate variables of the feature vector for each pattern:  
'-XYZ' is used to denote 3-axial signals in the X, Y and Z directions.

tBodyAcc-XYZ
tGravityAcc-XYZ
tBodyAccJerk-XYZ
tBodyGyro-XYZ
tBodyGyroJerk-XYZ
tBodyAccMag
tGravityAccMag
tBodyAccJerkMag
tBodyGyroMag
tBodyGyroJerkMag
fBodyAcc-XYZ
fBodyAccJerk-XYZ
fBodyGyro-XYZ
fBodyAccMag
fBodyAccJerkMag
fBodyGyroMag
fBodyGyroJerkMag

The set of variables that were estimated from these signals are: 

mean(): Mean value
std(): Standard deviation

Additional vectors obtained by averaging the signals in a signal window sample. These are used on the angle() variable:

gravityMean
tBodyAccMean
tBodyAccJerkMean
tBodyGyroMean
tBodyGyroJerkMean
