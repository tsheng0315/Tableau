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

You will get a table with all values of State in the first column and 
the number of rows of data that have these values in the second column. 

3. Right-click on a row-> “View Data” to see full data.  
Any ideas of what the numerical entries in the State field were likely supposed to represent (at
one point)?

###### Third:
Another quality check:
1. 'Sign in Count' on Rows. 
2. Un-aggregate the data.
You will see that there are some outliers in this variable. 

3. Right-click on the individual points to see the full data, 
note the pattern of data(most common character) displayed at this point. 

###### Forth:
Examine and exclude  outliers for further analyses.

1. Group together the outliers Dog IDs, filter them out of your analyses. 
2. Put the Dog ID field on Details of the Marks card. 

Group together all the data points that have Sign In Counts of above 175.

###### Fifth:
Exclude outliers Dog IDs from analyses:

3. 'Sign in Count' on Rows. 
4. Un-aggregate the data.
5. Drag Dog IDs(grouped) at Filter shelf 
6. Excluding all of the data points in the group with extreme values.
