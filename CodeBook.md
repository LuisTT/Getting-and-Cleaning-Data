Variables: 

x_training        - data set resulted from extraction of train/x_train.txt
y_training        - data set resulted from extraction of train/y_train.txt
training_subject  - data set resulted from extraction of train/subject_train.txt
x_test            - data set resulted from extraction of test/X_test.txt
y_test            - data set resulted from extraction of test/y_test.txt
test_subject      - data set resulted from extraction of test/subject_test.txt")
training          - data set resulted from merging training subect with activity and data
test              - data set resulted from merging test subject with activity and dat
all_data          - data set resulted from merging all data set
mean_sd_data      - data set resulted from extraction of mean and standard deviation for each measurement in all_data
activities        - data set resulted from extraction of activities data in activity_labels.txt
group_data        - data set resulted from gouping mean_sd_data by subject and activity
average_data      - data set resulted from summarization group_data to averages of each variable by subject and activity

procedures:

- definition the library to work: library(dplyr)
- Merge the train sets and test sets to create one data set as all_data
- convertion of text files in table sets captured and by respective variables
- column merge the training subect with activity and data
- column merge the test subject with activity and data
- row merge of all data set
- rename the relevant variables to extract
- extract a sub-set to a table of mean and standard deviation for each measurement
- take names for the activities in the data set
- update values with correct activity names
- create a new data set: gouped by subject and activity
- Change the variables names when summarizing the averages
- create and save a new data set as "average_data.txt"