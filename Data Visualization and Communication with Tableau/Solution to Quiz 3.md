## Hints for Week 3 Graded Quiz

Links:

https://www.coursera.org/learn/analytics-tableau/discussions/weeks/3/threads/zCedfoM-EemgVwpW7bTUyA

https://www.coursera.org/learn/analytics-tableau/discussions/weeks/3/threads/bJri_MMrEeirTw7nbK3LWA

#### Explanations for the graded quiz.
1. Use the dognition_data_no_aggregation data set

Data set description: 

https://d3c33hcgiwev3.cloudfront.net/_8d3c198be751a1f1f18ada7be82217f2_Dognition-Data-Set-Description.pdf?Expires=1595116800&Signature=OW8AHFcVSZKQBUgcVvNZuR75Xw~X3xVg90-86N1u3pZgI44Ws2FHQbtBqeTnA2EWRhwSS4sK7Z2CC0nfJTXVeMHXcbD2qb3MDETtxeMbYELF91KrtWC5a6S6SRyfpF30AB4zWYxgLbkqUFMb20sXqfwebdCSZ8H9S-9ijroaMps_&Key-Pair-Id=APKAJLTNE6QMUY6HBC5A

2. For all questions, filter out the test accounts: the Shih Tzu that weigh more than 190 pounds. 
Otherwise, will lead to inaccurate analysis.

#### Exclue Shih Tzu weigh 190: 

1. Right-click while in the Measure pane or go to Analysis. 
2. Choose Create Calculated Field...

**Function in Calculated Field**
Name: 'Shih Tzu 190' : 

IF [Breed]="Shih Tzu"
AND  [Weight]=190
THEN 'Shih Tzu 190'
ELSE 'View'
END

#### Q1
The greatest drop off happens after a subcategory of tests or while the subcategories of tests are in progress?

##### Tableau
Column: Rank by DogID
Rows: CNT(Number of records)
Filters: Shih Tzu 190: View
Mark Card: [Color: Subcategory Name]

<img width="700" height="500" src="https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-17%20at%2019.06.26.png"/>

##### Analysis
--> The highest four bar are mostly orange, the color is for the Empathy subcategory. 
The huge gap between the orange bar and others indicating a large decrease in the Empathy subcategory( in terms of counts of records). 

--> The graph shows most dogs dropped off after the Empathy subcategory. 

##### Q2

In the 'dognition_data_no_aggregation', after which game is the drop-off of completed tests the greatest?

##### Tableau
Column: Rank by DogID
Rows: CNT(Number of records)
Filters: Shih Tzu 190: View
Color: “Test Name”

--> Each color now represents a test name.
The largest difference is in the dark green color(4th bar, represents the Eye Contact game). 
Carefully examine each color in the 5th bar. There is no dark green at all.

##### Q3

If you remove all the entries associated with Shih Tzu dogs that weigh 190 pounds from the dognition_data_no_aggregation data set, how many different sequences of tests were administered to customers in the data that are left?

##### Tableau

Same as Q3

--> Point your cursor at the first bar and count the number of different colors in that bar. 
There are at least 4 different colors, meaning there are at least this many different sequences of tests.

##### Q4
During which day of the week do customers play Dognition games the most?

##### Tableau
Aggregation level: weekday

<img width="700" height="500" src="https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-17%20at%2020.49.58.png"/>

##### Q5
During which month in the data set were the most tests completed?

##### Tableau
Columns: Year(Created At), Month(Created At) / Column: Month(Correc...)

Rows: CNT(master_table)

Filters: Shih Tzu 190: View

<img width="700" height="500" src="https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-17%20at%2020.55.27.png"/>

##### Q6
After adjusting the time stamps 'dognition_data_no_aggregation' for time zone differences, which hour of the day do Dognition customers play the most amount of games?

##### Tableau

1. Add data source: "dognition_data_no_aggregation_with_zip_code_correction"
2. Edit blend data source: "dognition_data_no_aggregation_with_zip_code_correction"
3. Drag master table & time zone correction into worksheet

<img width="700" height="500" src="https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-17%20at%2021.06.34.png"/>

4. Create a calculated field to correct the hours.

**Formula: DATEADD("hour",[Diff from UTC],[Created at])**

Columns: HOUR(Corrected Created at)

Rows: CNT(Number of Records

Filters: Shih Tzu 190: View

<img width="700" height="500" src="https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-17%20at%2021.13.19.png"/>

#####  Q7
In the 'dognition_data_no_aggregation', approximately what percentage of users complete 20 tests?

##### Tableau 

Columns: Rank by DogID

Rows: CNTD(Dog ID)

Filters: Shih Tzu 190: View

Right-click on CNTD(Dog ID)-> "Quick Table Calculation..." -> "Percent of Total".


##### Q8
In 'dognition_data_no_aggregation', what percentage of users who begin with a “Free Start” complete 20 tests?

--> Very similar to Q7, except that you need to create a group variable that separate the free-starters from the non-free-starters.

##### Tableau
##### Group

Free Start User -> right click -> Create-> Group

Columns: Free Start User(Grouped), Rank by dogID

Rows: CNTD(DogID)

Filters: Shih Tzu 190: View

<img width="700" height="500" src="https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-17%20at%2022.05.18.png"/>

<img width="700" height="500" src="https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-17%20at%2022.05.44.png"/>

It seems that free start promotion didn't work as they thought.

Maybe Dognition should modify their marketing strategy. Eye Contact is the game where most dogs dropped off. 

##### Q9
Using the 'dognition_data_no_aggregation', rows: “Dog ID” and “Test Name”, Text: Created At, which of the following might be a value you would see in the column farthest to the right, if the “Created At”was blue and read SECOND(Created At)?

##### Tableau

Columns:

Rows: Dog ID, Test name

Text: Second(Corrected Created At)

##### Q10
When writing a calculation to rank each test a dog completed by its time stamp in 'dognition_data_no_aggregation', what's wrong with the rank table calculation: RANK(([Created At]),'asc')?

1. If simply place the Created At variable inside **RANK()**, Tableau will give you an error message.

2. Click on the triangle: "All fields must be aggregate or constants when using table calculation functions "

An aggregation before [Created At]is needed, the most appropriate of which is ATTR


##### Q11
You are writing a **calculation** to rank each test a dog completed by its time stamp in 'dognition_data_no_aggregation'. 

Partitioning: “Dog ID”,“Test Name” 

Addressing: “Second Created”

The resulting rank will:

**Analysis:**
The purpose: For each dog ID, rank the tests according to the order they were taken.
The calculation should achieve the same purpose as the **Ranked** *Dog ID*.

##### Tableau

**Rank** function:
* Name the calculation RANK 

* Rank(ATTR([Created at]),"asc")

* Place *RANK* in **Detail**. 

* Edit Table Calculation/ Compute Using--> Test Name

* Change Rank to Discrete. 

**Columns**:

**Rows**: Dog ID, Test name, RANK

**Text**: RANK

<img width="700" height="500" src="https://github.com/tsheng0315/Tableau/blob/master/Data%20Visualization%20and%20Communication%20with%20Tableau/image/Screenshot%202020-07-18%20at%2003.10.33.png"/>

##### Q12 
Write a calculation to create a column in a table that ranks each test a human user completed by its time stamp in 'dognition_data_no_aggregation'. 
The following fields will go in the Partitioning in your new calculation meant to rank each test a human user completed: 
Similar to Q11.

##### Tableau
Columns:

Rows: User ID, Test name

Filters: Dog ID (group), 

Text:  RANK



### Quiz 3
1. Use the dognition_data_no_aggregation data set provided in this course for this quiz.In the dognition_data_no_aggregation data set, 
the greatest drop offs of test-takers occur after a subcategory of tests is completed rather than while the subcategories of tests 
are still in progress. T/F

Answer: True

Comment: That graph shows that for those dogs that did not complete the 20 questions of the Assessment, most of them dropped off 
after they completed the Empathy subcategory. So, what do you think the answer to Q1 is? True or False. It should be easy to tell by 
now.


2. In the dognition_data_no_aggregation data set, after which game is the drop-off of completed tests the greatest?

Answer: Eye Contact Game

Comment: Each color now represents a test name. Using the same approach as in Q1 and each color from where it almost dominates the 
whole bar to where it is barely visible and compare the difference in Counts of Number of Records. You should find that the largest
difference is in the dark green color, the 4th bar that represents the Eye Contact game. Point your cursor to the 5th bar and carefully
examine each color. There is no dark green at all.So, what do you think the answer to Q2 is? Should be pretty easy

If you complete exercise 1 (Rank by DogID as a dimension and Number of records on the row shelf), just add a color filter on 
"Test Name" and look for the biggest drop in completed tests.

3. If you remove all the entries associated with Shih Tzu dogs that weigh 190 pounds from the dognition_data_no_aggregation data set, 
how many different sequences of tests were administered to customers in the data that are left?

Answer: at least 4

Comment:Examine the graph for Q2. Point your cursor at the first bar and count the number of different colors in that bar. 
There are at least 4 different colors, meaning there are at least this many different sequences of tests were administered to the 
customers after the test accounts are taken out. I think I gave you the answer on this one already.

4. During which day of the week do customers play Dognition games the most?

Answer: Sunday

Comments: set correct time column value to week. 

5. During which month in the data set were the most tests completed?

Answer: October 2014 

Comment: Point your cursor to the highest point of the graph and you should see the month Q5 is asking for.

6. After adjusting the time stamps of the tests completed by United States users provided in the “Created At” field of 
the dognition_data_no_aggregation data set for time zone differences, during which hour of the day do Dognition customers 
play the most amount of games?

Answer: 7 PM

Comment: Point the cursor to the highest point of the graph to find the hour that customers are most likely to play games with their 
dogs. It says 19. That's 24-hour format. Subtract 12 to get the PM hour.Isn't the answer to Q6 obvious now?

7.In the dognition_data_no_aggregation data set, approximately what percentage of users who begin taking the 
Dognition Assessment complete 20 tests?

Answer: 23% 

Comment:The bar chart at the bottom now has the percentage of dogs that completed each number of tests. To find out the percentage
that completed 20 tests, point your cursor at the bar of bottom bar chart that represented 20.
Isn't Q7 so easy that the credit is practically being handed to you for free?

8. In the dognition_data_no_aggregation data set, what percentage of users who begin taking the Dognition Assessment 
using a “Free Start” promotion complete 20 tests?

Answer: 6%

Comment:"1" means free-starters. At the bottom bar chart, in the part that has "1" on top, point your cursor to the bar for 20 
and you should see the percentage of free starters that completed all 20 tests.

9. Using the dognition_data_no_aggregation data set, if you make a table using the “Dog ID” and “Test Name” variables on the rows shelf, 
and Created At on the Text property of the Marks card, which of the following might be a value you would see in 
the column farthest to the right, if the “Created At” pill was blue and read SECOND(Created At)?

Answer: 0

Comment: The column after Test name have values of 0

10. Question 10: If you were writing a calculation to rank each test a dog completed by its time stamp in
the dognition_data_no_aggregation data set, what would be missing from the following version of your rank table 
calculation: RANK(([Created At]),'asc')

Answer: an aggregation before [Created At], the most appropriate of which is ATTR
Comments:After seeing the detail of this error message, you know immediately that the statement "there is nothing needed" should NOT be
selected.What about other statements?An aggregate function is needed. You always place the function in front of the variable. So, 
immediately, you can eliminate two more statements: "an aggregation after [Created At], the most appropriate of which is MEDIAN" & "an 
aggregation after [Created At], the most appropriate of which is ATTR " These two statements say that you should place the aggregate 
function after Created at, which is wrong.There are only two statements left. One suggests the MEDIAN function, the other suggests the 
ATTR function. Which one do you need if you are to write the RANK function? Think about what the MEDIAN function does and you will 
quickly conclude that MEDIAN is not the right aggregate function to mix with RANK.So, what statement should be chosen for Q10? 
After the analysis and eliminations above, there is only one possible answer left.

11. You are writing a calculation to rank each test a dog completed by its time stamp in the dognition_data_no_aggregation data set. 
You’ve configured your table calculation so that “Dog ID” and “Test Name” are in the Partitioning field 
and “Second Created” is in the Addressing field. The resulting rank will:

Answer: List “1” for the first test of every Dog ID

Comment:The purpose of writing a calculation here is to, for each dog ID, rank the tests according to the order they were taken. 
For every dog ID, the first test taken would receive the rank 1, the second would receive the rank 2 and so on. The calculation 
should achieve the same purpose as the Ranked by Dog ID field. Once you understand the purpose and function of the calculation, there 
is only "1" statement that stands out as the correct choice. (I put 1 inside double quotations to emphasize it. Combined with the 
analysis above, do you get the hint?)

12. You are writing a calculation to include a column in a table that ranks each test a human user completed
by its time stamp in the dognition_data_no_aggregation data set. You put this column directly to the left of the column you made 
to rank each test a dog completed by its time stamp. The following field(s) will go in the 
Partitioning field in the calculation configuration page in your new calculation meant to rank each test a human user completed: 
(check all that apply)

Answer: User ID

Comments: Q12 is very similar to Q11. Q11 uses Dog ID as a partition field. The ranking starts all over at each change of Dog ID. 
The only difference between Q11 and Q12 is that while Dog ID is used in Q11, User ID should be used in Q12. Please refer to my 
explanation for Q11 for the fine details.There is only one correct choice. With the above being said, isn't it obvious which choice 
is the correct one?

 
 
