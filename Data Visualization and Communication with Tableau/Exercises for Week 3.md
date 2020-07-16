### Goal: We are trying to increase the number of tests customers complete. 

The values in Total Tests Completed can only be understood at aggregation level of Dog ID,
while other variables we are interested in have a different level of granularity (such as at the level of individual tests

If you run into trouble with your visualizations, it’s probably
because you are trying to combine variables that are aggregated at/with different levels. 

#### Exercise 1
##### Q1:Removing entries that are infeasible data. 
(eg. Shih Tzus weigh 190 pounds (Shih Tzus typically weigh between 9 and 16 pounds). 

Solution:
Create a row calculation that can be used on Filter, to remove entries of Shih Tzus that weigh 190 pounds. 

This calculation should use IF/THEN/ELSE statement, with AND operator to output one value for each row 
that indicates whether the row belongs in “keep”/“exclude” category. 

For the rest of the exercises using the 'dognition_data_no_aggregation' data set, use this calculated field on the Filter to
exclude Dognition’s testing accounts from your analyses.

##### Q2: find out after which games users tend to drop out. 

To achieve this, we
need to use Rank by DogID.
It’s worth taking some time to understand exactly what this variable provides. 

Recall that
Dognition customers are given the tests in the same order each time (with a few exceptions
that Eliot told us about in the “Meet Your Dognition Data” video. 

To facilitate our initial
analyses, I ordered each test a dog took by its time stamp in Created At, and included the
rank the test received in this sorted order in its own variable called Rank by DogID. 

A
rank order of 1 in this field indicates the test described in that row of data was the first test
that dog took, a rank order of 5 in this field indicates that the test described in that row of
data was the fifth test the dog took, and so on.

I computed a similar rank for all the tests associated with a User ID. This rank, stored in
Rank by UserID, indicates the order of tests used by each human user. 

When a User ID is
only associated with one Dog ID, the values of Rank by DogID and Rank by UserID in a
row of data will be the same. 

When a User ID is associated with multiple Dog IDs, the
values of Rank by DogID and Rank by UserID in a row of data may differ. 

You will have
to aggregate these variables appropriately to extract the information you want.

The Total Tests Completed variable we used when analyzing the
dognition_data_aggregated_by_dogid data set last week was the maximum Rank by DogID
value associated with each Dog ID in the dognition_data_no_aggregation data set. 

This
week, when we need it, we will have to retrieve the maximum rank value associated with a
Dog ID ourselves through the level of aggregation we ask when using Rank by DogID.

To determine when users are dropping out of the Dognition test progression, make a bar
graph with Rank by DogID as a dimension on the columns shelf and Number of Records on
the Rows shelf. 

Remember, the Dognition tests are organized into subcategories of
cognitive abilities and personality attributes the tests are meant to assess (there are 5
subcategories in the first 20 tests comprising the Dognition Assessment). 

I highly
recommend that you place Subcategory Name or Test Name on Color. After which tests
do users tend to drop off? Do they drop off in the middle of the tests within a
subcategory, or at the end of all the tests associated with a subcategory? What could this
mean for Dognition?
