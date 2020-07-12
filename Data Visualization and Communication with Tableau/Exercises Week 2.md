## Practice Exercises for Week 2

Before starting to address analysis questions, it’s a good idea to get a feel for what our
data look like. To get started, I suggest you use the Row and Column shelves and the
Marks Card in the Tableau workspace to determine:

### Excercise 1
1) How many unique dogs are in the data set (indicated by the number of unique
entries in Dog ID)?
2) How many unique (human) users are in the data set (indicated by the number of
unique entries in User ID)?

#### Solution for Excercise 1
1. Dog ID/User ID on Rows. 
2. Measure-> Count(Distinct)

* As a discussion point, what does it mean if the number of unique User IDs is different
from the number of unique Dog IDs?
• A user may have many dogs

##### Steps when analyzing data set:
###### First:
Examine whether there are questionable values(mistakes or outliers)

1. Drag Country to Rows as dimension to see what countries are represented in data set.
2. Turn Country into **measure** and **aggregate** it by **Count(Distinct)** to see how many countries in total.
3. Do the same for State.
You will find that many entries in State have curious values! (real-world data sets can be messy)

###### Second: 
To get an idea of what some of the strange values might mean:
1. State on Rows
2. State aggregated by Count on Text of the Marks card. 

You will get a table with all values of State in the first column and the number of rows of data that have these
values in the second column. 

3. Right-click on a row-> “View Data” to see full data.  
Any ideas of what the numerical entries in the State field were likely supposed to represent (at
one point)?

###### Third:
Another quality check:
1. Sign in Count on the Rows. Then de-aggregate the data in the workspace through the “Analysis” menu.
You will see that there are some clear
outliers in this variable. 

right-click on the individual data points to see the raw data underlying them, 
note what columns of data seem to be common to all the rows displayed at this point. 
We will want to examine these outliers and possibly exclude them from future analyses.

Recall that one way to exclude outliers is to group together the individual Dog IDs that are
associated with all the extreme points on the graph, so that they can be filtered out of your
analyses. 
For that to be possible, you will need to put the Dog ID field on Details of the
Marks card. 
Note the difference between the raw data underlying the points you click on now, compared to before you put Dog ID on Details. 
Group together all the data points that have Sign In Counts of above 175.

We have confirmed that these Dog IDs represent test accounts that Dognition used to
troubleshoot their website. For the rest of the practice exercises using the
dognition_data_aggregated_by_dogid data set, exclude these Dog IDs from your analyses
by putting the grouped variable you just made on the Filter shelf and excluding all of the
data points in the group with extreme values.
