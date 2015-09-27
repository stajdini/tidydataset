## STEP 1: Merging  training and the test data to create one data set

# Saving data into data tables
subjectTrain = read.table("subject_train.txt")
subjectTest = read.table("subject_test.txt")
XTrain = read.table("X_train.txt")
XTest = read.table("X_test.txt")
yTrain = read.table("y_train.txt")
yTest = read.table("y_test.txt")

# adding column name for subject files
names(subjectTrain) = "subjectID"
names(subjectTest) = "subjectID"

# adding column names for measurement files
featureNames = read.table("features.txt")
names(XTrain) = featureNames$V2
names(XTest) = featureNames$V2

# adding column name for label files
names(yTrain) = "activity"
names(yTest) = "activity"

# combining files into one dataset called dataset
train = cbind(subjectTrain, yTrain, XTrain)
test = cbind(subjectTest, yTest, XTest)
dataset = rbind(train, test)


## STEP 2: Extracting only the measurements on the mean and standard
## deviation for each measurement.

# determining which columns contain "mean()" or "std()"
meanstdcols = grepl("mean\\(\\)", names(dataset)) |
      grepl("std\\(\\)", names(dataset))

# ensuring that we also keep the subjectID and activity columns
meanstdcols[1:2] = TRUE

# removing extra columns
combined = dataset[, meanstdcols]


# convert the activity column from integer to factor
combined$activity = factor(combined$activity, labels=c("Walking",
"Walking Upstairs", "Walking Downstairs", "Sitting", "Standing", "Laying"))


## STEP 3: Creating a tidy data set with the
## average measurements for each subject.
# load the reshape2 package (will be used in STEP 5)
library(reshape2)
# create the tidy data set
melted = melt(combined, id=c("subjectID","activity"))
tidydataset = dcast(melted, subjectID+activity ~ variable, mean)

# write the tidy data set to a file
write.table(tidydataset, "tidydataset.txt", row.names=FALSE)
