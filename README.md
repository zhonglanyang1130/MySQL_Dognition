# MySQL: Querying Dognition Database

In this data infrastructure project, I helped Dognition (https://www.dognition.com) to examine their data, identify potential issues, and provide some general insights regarding their product and users. The querying language I used is MySQL Workbench.

# Dataset
The dataset came from Dognition's undisclosed internal database.

There were 6 data tables in the database that contains records about registrated users & dogs, results of dog ability exams of each dog, exam ratings of users, different memebrships, date & time information for exams and membership registration.

# Tasks:
Three tasks were completed in this project: data cleaning, examine potential issues, analyzing data.

#Task 1: Broad Data Cleaning and Relational Schema
The Dognition team was awared that their database is somewhat “messy” but they are unclear about the extent of the problems. 
I organized the six data tables by removing all the duplicates, determine and verify the primary key for each of the data table.

## Relational schema:
![relational schema](https://user-images.githubusercontent.com/129545791/229343076-df5d9e09-d24a-44dc-9c70-8b2cc94b3e47.png)

# Task 2: Searching for Potential Issues
I exmained potential issues and inconsistencies.
## problems for complete_tests
1. user_guid is NULL for every record, which indicates Unique ID for user is useless in the table.
2. contains records where dog_guid is also NULL, which make no sense as it does not contain information as to which dog has done the test.
## problems for dogs
1. weight column contains 0 instead of NULL value for an unknown weight, as weight being 0 for a dog does not make much sense.
2. dimension column contains mixed of NULL and empty value for unknowns.
3. As the description for dimension suggests, it is one of Dognition's 9 personality profiles, a more descriptive field name could be given for personality profiles instead of dimension, which could be misleading as one might think dimension may suggests the size of the dog.
4. breed_group contains mixed of NULL and empty value for unknowns.
5. mean_iti_days and median_iti_days contains mixed of NULL value and string "NaN" for unknowns, which makes the type of field as VARCHAR
6. mean_iti_minutes and median_iti_minutes contains #VALUE! 
7. The type of birthday is supposed to be DATETIME, but it is VARCHAR
8. The types of time_diff_between_first_and_last_game_days and time_diff_between_first_and_last_game_minutes are VARCHAR, but the differnce between time should also be double

## problems for exam_answers
1. subcategory_name contains category that is not listed in the "data dictionary".
2. subcategory_name and test has exactly same value.
3. As indicated in the "data dictionary" step_type is key for whether the test item was a question or a stopwatch, so not exactly sure what bark means.
4. loop_number contains negative number, which does not make sense.

##problems for reviews
1. rating has NULL value, but a user was supposed to give a rating between 1 to 9, so it does not make sense to record a rating that an user have not given a rating.

“problems” for site_activities
1. member_id contains NULL value
2. category_id contains NULL value

##problems for users
1. According to "data dictionary", membership_id is an Unique ID, but in the table, membership_id contains many duplicates.
2. utc_correction contains mixed of NULL and #N/A value.
3. city, state, zip and country all contain mixed of NULL and N/A value.

# Task 3: Analyzing data
Joined data tables for analyzing the porportion of users signed up for different membership types per month every year.

Investigate the correlation between year and month of joining, membership types, and number of tests completed for each membership types.

## Key findings:
Other findings include:
1. Among the users who provided their geographical information, users from urban area in US are more likely to complete the assessment tests.

2. The percentage of script_detail_id within 400-499 (HTTP bad request) is only around 4% which means that the website issue may not be the potential issue as well.

3. Overall the female dog complete more tests than male dog. Among the dogs with known breed_group or breed_type, male sporting pure breed has the highest number of tests completed. We can conclude that cross breed and sporting pure breed better suited the assessments as they have completed the greatest number of tests.

More included in the jupyter notebook file.
