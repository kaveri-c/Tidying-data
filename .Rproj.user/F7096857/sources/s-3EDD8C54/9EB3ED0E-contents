library(dplyr)
#1. Merges the training and the test sets to create one data set.
X_train <- read.table("./train/X_train.txt")
y_train <- read.table("./train/y_train.txt")
X_test <- read.table("./test/X_test.txt")
y_test <- read.table("./test/y_test.txt")
y_test <- read.table("./test/y_test.txt")

X <- rbind(X_train, X_test)
y <- rbind(y_train, y_test)

#2. Extracts only the measurements on the mean and standard deviation for each measurement.
features <- read.table("./features.txt")
logical <- grepl("-mean\\(\\)-|-std\\(\\)",features[,2])
indices <- which(logical)
df <- select(X, indices)

#3. #Uses descriptive activity names to name the activities in the data set
labels <- read.table("./activity_labels.txt")
y$V1 <- ordered(y$V1, levels = labels[,1], labels = labels[,2])


#4. Appropriately labels the data set with descriptive variable names.
colnames(df) <- features[indices,2]
colnames(y) <- "activity"


#5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each (subject.) 
subject_train <- read.table("./train/subject_train.txt")
subject_test <- read.table("./test/subject_test.txt")
subject <- rbind(subject_train, subject_test)
colnames(subject) <- "subject"
df <- cbind(df,subject)
df <- cbind(df,y)

new_data <- group_by(df, subject, activity)
mean_data <- summarize_at(new_data, vars(-activity, -subject), funs(mean))
