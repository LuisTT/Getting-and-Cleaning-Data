# Just run the script: run_analysis.R with the project files in the working directory

# defining the library to work

library(dplyr)

# Step 1: Merges the training and the test sets to create one data set.
# read the text files to data sets 
# Merge the train sets and test sets to create one data set as all_data

#convert text files in table sets captured by respective variables
x_training <- read.table("train/x_train.txt")
y_training <- read.table("train/y_train.txt")
training_subject <- read.table("train/subject_train.txt")

x_test <- read.table("test/X_test.txt")
y_test <- read.table("test/y_test.txt")
test_subject <- read.table("test/subject_test.txt")

# column merging training subect with activity and data

training <- cbind (training_subject, y_training, x_training)

# column merging test subject with activity and data

test <- cbind (test_subject, y_test, x_test)

# row merging all data set

all_data <- rbind (training, test)

# Step 2: Extracts only the measurements on the mean 
# and standard deviation for each measurement.

# renaming the relevant variables to extract

colnames(all_data)[1:8] <- c("subject", "activity", "mean_x", "mean_y", "mean_z", "std_x", "std_y", "std_z")

# extracting a sub-set the table to the 
# mean and standard deviation for each measurement

mean_sd_data <- select(all_data,subject:std_z)

# Step 3: Uses descriptive activity names to name the activities in the data set

# naming the activities in the data set

activities <- read.table("activity_labels.txt")

# update values with correct activity names

mean_sd_data[, 2] <- activities[mean_sd_data[, 2], 2]




# Step 4: Appropriately labels the data set with descriptive variable names.

# Step 5: From the data set in step 4, creates a second, 
# independent tidy data set with the average of each variable 
# for each activity and each subject.

# new data set: gouped by subject and activity

group_data <- group_by(mean_sd_data,
                         subject,
                         activity)

# Changing the variables names when summarizing the averages
average_data <- summarize(group_data,
                          Average_mean_x=mean(mean_x),
                          Average_mean_y=mean(mean_y),
                          Average_mean_z=mean(mean_z),
                          Average_std_x= mean(std_x),
                          Average_std_y= mean(std_y),
                          Average_std_z= mean(std_z))

# create and save a new data set as "average_data.txt"

write.table(average_data, "average_data.txt", row.name=FALSE)

View(average_data)

