## Dynamic Data Manipulation and Presentation in Tableau
### Goal: Increase the number of tests customers complete. 

Use dognition_data_no_aggregation” data set

Can not combine variables that are aggregated at/with different levels. 
(The values in Total Tests Completed can only be understood at aggregation level of *Dog ID*,
while other variables we are interested in have a different level of granularity (such as at the level of individual tests

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
(use *Rank by DogID*. )

Tests are given in the same order each time. 

Order each test a dog took by its time stamp in *Created At*. 
*Rank by DogID*:
A rank order of 1 indicates the test was the first test that dog took,
a rank order of 5 indicates the test was the fifth test the dog took.

Same for *User ID* and *Rank by UserID*, indicates the order of tests used by each human user. 

When a *User ID* is only associated with one *Dog ID*, the values of *Rank by DogID* and *Rank by UserID* in a
row will be the same. 

When a *User ID* is associated with multiple *Dog ID*s, the values of *Rank by DogID* and *Rank by UserID* in a row may differ. 

You will have to aggregate these variables appropriately to extract the information you want.

The *Total Tests Completed* in 'dognition_data_aggregated_by_dogid' is the maximum *Rank by DogID*
value associated with each *Dog ID* in 'dognition_data_no_aggregation'. 

Need to retrieve the maximum rank value associated with a *Dog ID* through the level of aggregation we ask 
when using *Rank by DogID*.

Columns: *Rank by DogID* 
Rows: *Number of Records* ( DogID(count) )

The Dognition tests are organized into subcategories of cognitive abilities/personality.
(5 subcategories in the first 20 tests comprising the Dognition Assessment). 

I highly recommend that you place *Subcategory Name* or *Test Name* on **Color**. 
After which tests do users tend to drop off? 
Do they drop off in the middle of the tests within a subcategory, or at the end of all the tests associated with a subcategory? 
What could this mean for Dognition?
