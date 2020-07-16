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

![image](https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-16%20at%2013.03.15.png)

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
![im](https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-16%20at%2013.44.57.png)

**Use Tableau’s date hierarchy** 

##### Analysis: 
1. Which days of the week are customers likely to play the games? (Use “weekday” level on the date hierarchy)
![im](https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-16%20at%2014.03.01.png)
2. Which hours of the day are customers likely to play the games (Use “hour” level on the date hierarchy)?
![im](https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-16%20at%2014.05.32.png)

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
adjusted date
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
![](https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-16%20at%2015.03.32.png)
2. Do those hours change at different times of the week? 
![](https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-16%20at%2015.06.33.png)
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
![]{height=500px width=500px}(https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-16%20at%2021.34.09.png)

3. 
**Columns**: *Free Start User(Group)*, *Rank by DogID*. 
**Rows**: *Put Dog ID*(Count (distinct) ). 

It looks like perhaps *Free Start* users do not finish as many tests as *non-Free Start*users, but it’s hard to know for sure because there are so many fewer *Free Start* users to start with. 
A more direct way to assess the success of *Free Start* users would be to compute a table calculation that would tell you what percentage of users who start the
Dognition Assessment make it to each test along the way. 

Without removing any of the pills you currently have on the Columns or Rows shelves,
drag another instance of *Dog ID* to the **Rows** shelf. 
Click on the drop down and choose quick table calculation option, followed by “percent of total.” 
You should now have one set of bar charts that show you the raw numbers of dogs who completed a certain number
of tests, and a second set of charts that show you what percentage of a total those raw numbers represent.
The goal in making the table calculation was to determine what percentage of those who
start their Dognition experience with a free start finish each number of tests. 
Do the charts you see depict that? Probably not, because the calculated field is likely making
calculations with all the data in the work space together at the same time, rather than
doing the calculation separately for different partitions within the work space. 
You have to tell Tableau what partitions the table calculation should take into account. 
To do this, click on the table calculation to edit it. 
Can you figure out how to set the advanced options so that the table calculation computes percentages separately for Free Start users
vs non-Free Start users? 
Do you think the *Free Start* tests seem to be working as intended?

#### Exercise 4
In this exercise, we are going to use table calculations to determine how we could use Tableau to
dynamically recreate the ranks stored in the Rank by DogID and Rank by UserID variables.
These variables, remember, chronologically rank each test according to its associated time
stamp in Created At, and restart the ranking either for every dog or for every customer.
To begin, make a group of Dog IDs that only has a few Dog IDs included (randomly
choose 4 or 5 DogIDs). Use your new grouped variable and the filter shelf to ensure that
you only analyze the data from the few dogs you chose in your workspace. This will make
troubleshooting your calculations much faster.
Next, place Dog ID on the rows shelf, followed by Test Name on the right-hand side.
Then put Created At on Text, and adjust the variable aggregation so that you get a level of
detail that is appropriate for the purpose of the exercise. You should see a table with Dog
ID in the left-most column, Test Name in the column to the right of that, and the time the
test was created in the right-most column.
Our goal is going to be to create a column between the Test Name and Created At columns
that uses a calculation (NOT Rank by DogID – that would be cheating!) to indicate the
ranked order each test was completed, sorted from 1 to the last test taken. To achieve this,
make a calculation that starts with RANK, and then drag the Created At pill from your
workspace into the parentheses Tableau automatically inserts in your calculated field.
Notice that Tableau will likely insert a date function with the level of detail you specified
on the Created At pill in your table. You will need to choose whether the rank should be
ascending or descending.
As you troubleshoot your calculation, think carefully about whether the variables in your
calculation need to be aggregated, and if so, how. Also think about what level of detail of
the time stamps provided in Created At would be most useful.
Once you have a valid calculation, drag it to Details. Then right-click (control-click) to
edit the calculation, and navigate to the “Compute Using” screen. Chose the options you
think are most appropriate for your goals. Once selected, convert the pill to a dimension
and place it in the appropriate place on the Rows shelf. Assess whether your calculation
succeeded by comparing your rank to the rank provided in Rank by DogID.
Can you make a similar calculation that ranks the tests completed by each human user,
mimicking the information provided in Rank by UserID? Can you figure out how to
include both ranks in the same table?


