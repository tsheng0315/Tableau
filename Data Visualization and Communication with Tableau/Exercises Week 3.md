## Week 3: Dynamic Data Manipulation and Presentation in Tableau
### Goal 1: Increase the number of tests customers complete. 
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

1. *Created At*: The order of tests a dog took(ranked by time stamp of the test). 
2. *Rank by DogID*:
A rank order of 1 -> the test was the 1st test that dog took,
A rank order of 5 -> the test was the 5th test the dog took.

3. *Rank by UserID* -> The order of tests used by each human user. 

a) When a *User ID* is only associated with one *Dog ID*, the values of *Rank by DogID* and *Rank by UserID* in a
row will be the same. 

b) When a *User ID* is associated with multiple *Dog ID*s, the values of *Rank by DogID* and *Rank by UserID* in a row may differ. 

You will have to aggregate these variables appropriately to extract the information you want.

4. *Total Tests Completed* in 'dognition_data_aggregated_by_dogid' =
the maximum *Rank by DogID* value (associated with each *Dog ID*)in 'dognition_data_no_aggregation'. 
##### tableau

**Columns**: *Rank by DogID* 

**Rows**: *Number of Records* (DogID(count))

The Dognition tests are organized into subcategories of cognitive abilities/personality.
(5 subcategories in the first 20 tests comprising the Dognition Assessment). 

**Color**: *Subcategory Name*/*Test Name* 

<img width="500" height="500" src="https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-16%20at%2013.03.15.png"/>

**Q**:
1. After which tests do users tend to drop off? 
2. Do they drop off in the middle of the tests within a subcategory, or at the end of all the tests associated with a subcategory? 
3. What could this mean for Dognition?


#### Exercise 2

**Aim 2**: 
To better target advertisements, need to know when customers tend to play the Dognition games. 

*Created At* has a time stamp of every test recorded by a customer.

##### Tableau: 
**Columns**: *Created At*

**Rows**: *Number of Records*

<img width="500" height="500" src="https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-16%20at%2013.44.57.png"/>

**Use Tableau’s date hierarchy** 

##### Analysis: 
1. Which days of the week are customers likely to play the games? (Use “weekday” level on the date hierarchy)
<img width="500" height="500" src="https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-16%20at%2014.03.01.png"/>
2. Which hours of the day are customers likely to play the games (Use “hour” level on the date hierarchy)?
<img width="500" height="500" src="https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-16%20at%2014.05.32.png"/>
**Q**: Does anything look suspicious to you? 

**A**: Many games are played at mid-night, doesn’t make sense. 

**Reason**: The time stamps are provided in “Coordinated Universal Time” (UTC) and do not take time zones/daylight savings into account. 

**Solution**: 
1. find a UTC correction data set t0 provide correction for every entry in our location-related variables
2. blend the secondary data set with 'dognition_data_no_aggregation'.

Use **joining** method, to combine 'UTC corrections for a collection of United States zip codes' data set with 'dognition_data_no_aggregation'. 
(The results of a joining will be easier to work with than the results of data blending.)

**New data set**: 
'dognition_data_no_aggregation_with_time_zone_correction':
1. “master table”: the original 'dognition_data_no_aggregation'
2. “timezone correction” : zip code correction data

Drag both worksheets to the box where it says “drag sheets here”. 
left: “master table” 
right:“time zone correction”

Click on the circles and change the default from “inner” to “left join.”

(Left join: retain all the data from the master table, and incorporate data from 'time zone correction' when there is a zip code that matches between the two files.)
You will see that *Diff from UTC* below “time_zone_correction” worksheet. 

Make a row calculation that will adjust each value of *Created At* by the correction provided in *Diff from UTC*.

use the **DATEADD** function in your calculated field:
adjusted date：
DATEADD('hour',[Diff from UTC],[Created at])

**columns**: 'adjusted date'

**rows**: count of records

Keep 'adjusted date' as a dimension, so that it is at the level of “hour” in the date hierarchy. 

Right-click on the “Null” subheading and choose “Hide”.

You should be able to see the original version of *Created At*, the new corrected version of *Created At*
(title of the calculated field)for each row. 

When you are confident your calculation is correct, you are ready to interpret your new, time-zone corrected results. 
To aid in this, bring another copy of *(Corrected)Created At*  to **filter**. 
Choose the options that allow you to filter by “Weekdays.”

##### Analysis:
1. What hours of the day do customers tend to play games? 
<img width="500" height="500" src="https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-16%20at%2015.03.32.png"/>
2. Do those hours change at different times of the week? 
<img width="500" height="500" src="https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-16%20at%2015.06.33.png"/>
3. When you should send advertisements to customers?

#### Exercise 3
**Q**: Assess whether the “Free Start” promotions worked.
*Free Start User*:
1: Yes
0/Null: No
**Steps**:
1. Determine whether the user began their Dognition experience with a free start. 

Grouping: Group *Free Start User* into “Free Start”/“non-Free Start” .

2. Get an idea of how many data points you have for both categories(Visualization & Marks Card). 
Examine when *Free Start users* were enrolled, and how many *non-Free Start users* were enrolled at the same time.

<img width="500" height="500" src="https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-16%20at%2021.34.09.png"/>

##### Tableau

**Columns**: *Free Start User(Group)*, *Rank by DogID*. 

**Rows**: *Dog ID*(Count (distinct) ).

Free Start users:
<img width="500" height="500" src="https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-16%20at%2021.41.36.png"/>

non-Free Start users:
<img width="500" height="500" src="https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-16%20at%2021.52.24.png"/>

**Analysis**: 
1. It seems *Free Start* users do not finish as many tests as *non-Free Start*users, but it’s hard to know for sure because there are fewer *Free Start* users to start with. 

2. To better assess the success of *Free Start* users, compute a table calculation on percentage of users in two subcategories. 

**Rows**: *Dog ID* 

Second CNTD(DogID)-> Edit Table Calculation-> 'percent of total'-> Specific Dimension -> Rank by DogID (addressing fields).
**partition**: The table calculation is performed separately within each partition.
**addressing**: Determine the direction of the calculation

Free Start users:
<img width="500" height="500" src="https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-16%20at%2023.42.07.png"/>

non-Free Start users:
<img width="500" height="500" src="https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-16%20at%2023.42.26.png"/>

One bar chart shows you the raw data, and a second chart shows you the percentage of a total those raw numbers.
The chart shows what percentage of those who start their Dognition experience with a free start finish each number of tests. 

3. 1.07% of free-starters finished the 20-question Assessment, while 2.57% in non-free-start users. 

#### Exercise 4
Use table calculations to determine how we could dynamically recreate the ranks stored in the *Rank by DogID* and *Rank by UserID*.

##### Tableau
**rows**: *Dog ID*,*Test Name* 

**Text**: *Created At* (aggregation level up to you)

**Result table**-> *Dog ID* + *Test Name* + time test was created.

**Next**: Use calculation, create a column between *Test Name* & *Created At* columns, to indicate the ranked order each test completed (from 1 to the last test taken). 

**Make a calculation**:
Mimic rank 

1. RANK(ATTR([Created at]),'asc') 

a. think whether the variables in your calculation need to be aggregated, and if so, how. -->ATTR()

b. think what level of detail of the time stamps in *Created At* would be most useful.

c. For level of details, select the Minute. (lots of tests were created during the same hour. If "Hour" is selected, ranking might not work.)

2. **Details**: Mimic rank 

3. Edit calculation, navigate to the “Compute Using”. 

##### Tableau
**Rows**: Dog ID, Test name, Mimic rank 
Text: Minute(Created at) 
-->Edit Table Calculation
-->Specific Dimensions: *Minute of Created At*, *Test Name*.
--> Convert the calculated field to dimension by selecting Discrete.
--> Place the calculated field in the Rows shelf, behind Test Name.
<img width="500" height="500" src="https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-17%20at%2001.16.58.png"/>

Links:
https://www.coursera.org/learn/analytics-tableau/discussions/weeks/3/threads/yrDl_sMvEeiALwrKWTa7ig
https://www.coursera.org/learn/analytics-tableau/discussions/weeks/3/threads/kpBB3nPmEeiPrBLBSH_lGA


