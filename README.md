CourseProject: Getting and Cleaning Data
=======================================

This repo is essentially for the data scientist's, getting and cleaning data course project

The data analysis code is show below althought it is also shown in a separate file named run_analysis.R which you can find in this repo. 
The aim of this excercise is to merge two data sets from a wearable computer experiment. Each data set is scattered in different files. So, it is first required to collect each data set and set labels to its values in addition to give descriptive names to their variables.

The analysis approach is to (1) first read the test and train data sets, merge each one with its subject table in order to match the experiment subjects to their readings. (2) use features.txt file to give descriptive names to the test variables (3) unify the names in the two data sets (train and test) and merge them using rbind. (4) use aggregate() function to create a final data set with the average of each variable for each activity and each subject.

##Reading the data set different txt files

#read the features file which will be used to set the variable names for the final merged data frame
features<-read.table("./R/UCI HAR Dataset/features.txt")
#read the test data
x_test<-read.table("./R/UCI HAR Dataset/test/X_test.txt")
#read test data acivities 
y_test<-read.table("./R/UCI HAR Dataset/test/Y_test.txt")
#read test subjects
subject_test<-read.table("./R/UCI HAR Dataset/test/subject_test.txt")
#read train subjects
subject_train<-read.table("./R/UCI HAR Dataset/train/subject_train.txt")
#read the train data
x_train<-read.table("./R/UCI HAR Dataset/train/x_train.txt")
#read train data activities
y_train<-read.table("./R/UCI HAR Dataset/train/y_train.txt")
#read activity labels
activity_labels<-read.table("./R/UCI HAR Dataset/activity_labels.txt")
#initial column names in order to bind the subject and activity data set to the main test and train data sets

##Set column names and add subjects and activities to their data sets (train and test)
colnnames(subject_test)<-"subject_test"
colnames(subject_train)<-"subject_train"
colnames(y_train)<-"y"
colnames(y_test)<-"y"
#add subject test  and activities to the raw test data set
test<-cbind(subject_test,y_test,x_test)
#add subject test  and activities to the raw train data set
train<-cbind(subject_train,y_train,x_train)
features$V2<-as.character(features$V2)
#to give descriptive variable names as required in part 4 in the assignment
colnames(test)[3:563]<-features$V2
colnames(train)[3:563]<-features$V2
#add descriptive labels to activity as required in part 3. the labels are extracted from activity_label
test$y_test<-factor(test$y_test, levels=c(1,2,3,4,5,6), labels=activity_labels$V2)
train$y_train<-factor(train$y_train, levels=c(1,2,3,4,5,6), labels=activity_labels$V2)
#change column names in order to match them in the two data sets (train and test), which is required to merge the data using rbind
colnames(test)[1:2}<-c("subject","activity")
colnames(train)[1:2<-c("subject","acitivity")
                
##Merge the two data sets
MergedData<-rbind(test,train)


#select columns with mean or standard deviation for each measurement
selectedCols<-grep("[Mm]ean|[Ss][Tt][Dd]",names(MergedData))
MedgedData2<-MergedData[,c(1,2,selectedCols)]


#part 5 the final data set with the average of each variable for each activity and each subject is stored in number5
number5<-aggregate(MergedData2[,3:88],by=list(MergedData2$activity,MergedData2$subject),FUN=mean)

#save the final data set in .txt file
write.table(number5, file="final_data_summary.txt")
