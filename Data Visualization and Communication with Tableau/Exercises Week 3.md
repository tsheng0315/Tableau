## Dynamic Data Manipulation and Presentation in Tableau
### Goal: Increase the number of tests customers complete. 
(data set: 'dognition_data_no_aggregation')

Can't combine variables that are aggregated at/with different levels. 
(The values in *Total Tests Completed* can only be understood at aggregation level of *Dog ID*,
different level of granularity, such as level of individual tests

#### Exercise 1
##### Q1:Removing entries that are infeasible data. 
(eg. Shih Tzus weigh 190 pounds (Shih Tzus typically weigh between 9 and 16 pounds). 

##### Solution:
1. Create a row calculation that can be used on Filter, to remove entries of Shih Tzus that weigh 190 pounds. 

This calculation should use IF/THEN/ELSE statement, with AND operator to output one value for each row 
that indicates whether the row belongs in “keep”/“exclude” category. 

2. Using the 'dognition_data_no_aggregation' data set, use this calculated field on the Filter to
exclude Dognition’s testing accounts from your analyses.

##### Q2: Find out after which game users tend to drop out. 

Tests will be given in the same order each time. 

*Created At*: The order of tests a dog took(ranked by time stamp of the test). 
*Rank by DogID*:
A rank order of 1 -> the test was the 1st test that dog took,
A rank order of 5 -> the test was the 5th test the dog took.

*Rank by UserID* -> The order of tests used by each human user. 

a) When a *User ID* is only associated with one *Dog ID*, the values of *Rank by DogID* and *Rank by UserID* in a
row will be the same. 

b) When a *User ID* is associated with multiple *Dog ID*s, the values of *Rank by DogID* and *Rank by UserID* in a row may differ. 

You will have to aggregate these variables appropriately to extract the information you want.

*Total Tests Completed* in 'dognition_data_aggregated_by_dogid' =
the maximum *Rank by DogID* value (associated with each *Dog ID*)in 'dognition_data_no_aggregation'. 

**Columns**: *Rank by DogID* 
**Rows**: *Number of Records* (DogID(count))

The Dognition tests are organized into subcategories of cognitive abilities/personality.
(5 subcategories in the first 20 tests comprising the Dognition Assessment). 
**Color**: *Subcategory Name*/*Test Name* 

**Q**:
After which tests do users tend to drop off? 
Do they drop off in the middle of the tests within a subcategory, or at the end of all the tests associated with a subcategory? 
What could this mean for Dognition?




