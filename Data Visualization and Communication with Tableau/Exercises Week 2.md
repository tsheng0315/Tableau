## Practice Exercises for Week 2

Before starting to address analysis questions, it’s a good idea to get a feel for what our
data look like. To get started, I suggest you use the Row and Column shelves and the
Marks Card in the Tableau workspace to determine:

### Excercise 1
Have a feeling for what our data look like

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

note: I was able to get around this issue by putting sign in count on rows, Dog ID on detail, 
and then right clicking on the axis --> edit axis --> fixed --> select 0 - 175.
once the axis is restricted then I manually drag selected (hold left click) data and made a group. 
Then i could put this dog id group in the filter card and it works.

### Exercise 2
Start addressing some of the questions in analysis plan: 
* Make a recommendation to Dognition, to increase the number of tests customers complete. 
1. Identify the features of dogs/their owners that have correlated with increased completion scores in
the past.

(The 'dognition_data_aggregated_by_dogid' provides data about the total number of tests completed by each dog
and/or human customer (as opposed to about each test completed).)

Aim 1: Examine features of dogs that correlate with differences in the number of tests the dogs complete. 

1. Total Tests Completed: the total number of tests customers completed. 
2. The mean and median “ITI” : in minutes/hours for the tests each dog completed, 
3. Inter-test interval: time elapsed between the first and last tests each dog completed.

Aim 2: Address how personalities and breed of dogs affect completion metrics
1. Make visualizations with any of the variables described above, and Breed Type, Breed Group, Dimension variables. 
2. Try different combinations of dependent variables and independent variables in the Rows and Columns and/or Marks card. 
3. Types of Breeds & types of Personality.

'Dimension' can only be assigned to dogs after they have completed the first 20 tests.
* Tableau
Columns:Breed Type
Rows: Median(Total Tests Complete)
* Anaylsis:
1. Average total tests completed were very similar across breed types
2. Except for Pure Breeds, the overwhelming majority of entries is missing a breed group label(0)
3. Median Total Tests Completed for all Breed Types is around 7.

### Exercise 3
• Owners’ personalities & possiblity to complete all tests
• Variable: Total Tests Completed, Breed Type, Dog Fixed, DNA Tested, Total Tests Completed. 

Owners who get their dogs DNA-tested are likely to:
(a) confirm whether or not the dog is pure-bred
(b) find out about where their dog came from (http://www.caninejournal.com/dna-testing-for-dogs/).
such owners are curious and are more likely to complete Dognition tests than other customers.

breed type (pure-bred, mixed or unknown origin...) & whether or not the owner intended to 
breed the dog (which would be impossible if the dog were fixed(spayed/neutered)). 
Owners who intend to breed dogs are more interested in the personality of dogs.

### Exercise 4
•Aim: Whether customers in particular countries and/or states in the US have more testthan others. 
•Aim: Whether customers in specific geographic regions are more likely to complete more tests. 

Find out what countries Dognition users come from. 
How many distinct dogs have been tested in each country. 
1. Rows: MEDIAN(Total Tets Complete) CNTD(Dog ID)
2. Country on the **Columns**.

• Analysis 
The median of Total Tests Completed and distinct count of Dog ID for each Country. 
Germany, Denmark, Norway and New Zealand have higher median Total Tests Completed than the US.


Too many countries -> map chart -> each country is colored by how many dogs have been tested there

From graph we can see, most customers are located in the US. 
Filter : only US records. 
Are there any states that clearly have more customers than others?

Next let’s examine whether there are any states that have customers that are more or less
likely to complete their tests. 
Rows: Total Tests Completed. 
The median and average numbers of tests completed seem to be higher. 

• Tableau
Use Country: group 1 the US; group 2 the rest countries.
Total Tests Completed & new Country (grouped) variable. 

Q: Use the information to make a recommendation about a geographical market should nurture ?

In terms of marketing and long-term business strategy, wile it is of Dognition's interest to continue focusing on the above geographical 
markets, it may also want to expand more into other dog-friendly countries, such as France, Norway and Luxembourg. 

#### Exercise 5
Aim: Assess the hypothesis that customers who complete tests quickly are more likely 
to complete more tests overall. 

variables: Median ITI and Mean ITI. 
I took all the time-stamps from the test records of a given Dog ID in a separate data set (which we will use next week), 
and computed the amount of time between the time-stamp of each test. That gave me a collection of intertest intervals for each dog.

If a dog completed 20 tests, I recorded the mean and median of 19 inter-test intervals.
However, since the dognition_data_aggregated_by_dogid data set has the data aggregated
at the level of Dog ID, not at the level of individual tests, we can’t just filter out all the
data associated with tests 20-45. 

We have to filter out all the data from dogs who completed 20 or more tests. 
(a) we will throw out some data in this analysis that could have otherwise been useful,
and (b) our analyses will be biased towards dogs who do not complete all the Dognition Assessment tests, which might not translate
well to dogs who do finish the Dognition Assessment tests. 

Address our question about completion rate by running a set of regressions treating Total Tests Completed as a measure. 
filter out all of the data from dogs who completed 20 or more tests.
Columns: Total Tests Completed
Rows: Median ITI; Mean ITI; un-aggregate the data
add a trend line 
observe that the trend lines appear to go in opposite directions. How can that be? 
--> outliers

How outliers can affect regression lines:
http://stattrek.com/regression/influential-points.aspx?Tutorial=AP
http://discuss.analyticsvidhya.com/t/effects-of-outliers-on-regression-model/2403/2
What do you think the best interpretation of these results are? 
Would these results influence any recommendations you make to Dognition? 

