# Microsoft DataCamp

## Introduction to Python for Data Science_Final Lab

### Section 2

#### Exercise

##### Creating Columns I

If you look at the dataset, you'll notice that while there's a column which shows the percentage of women in each department, there is no column which shows the percentage of men.

##### Instructions

Create a new column named sharemen, that contains the percentage of men for a given department by dividing the number of men by the total number of students for each department.

##### Script.py

```python
#Add sharemen column
recent_grads['sharemen'] = recent_grads['men'] / recent_grads['total']
```

#### Exercise
##### Select Row with Highest Value
Remember how you found the row of data with the highest percentage of women? Now you'll find the row that corresponds to the department with the highest rate of men.

The module numpy has been imported under the alias np for you.
##### Instructions
- Using numpy, find the maximum value for the percentage of men and call this variable max_men.
- Select the row that has the percentage of men which corresponds to max_men.

##### Script.py
```python
#Find the maximum percentage value of men
max_men = np.max(recent_grads['sharemen'])

#Output the row with the highest percentage of men
print(recent_grads[recent_grads['sharemen'] == max_men])
```

#### Exercise
##### Creating columns II
Eventually you want to figure out which departments are most balanced between men and women. To accomplish this, you'll add a new column that reports the difference in percentages between men and women.
##### Instructions
Add a column named gender_diff that reports how much higher the rate of women is than the rate of men.
##### Script.py
```python
#Add gender_diff column
recent_grads['gender_diff'] = recent_grads['sharewomen']-recent_grads['sharemen']
```

#### Exercise
##### Updating columns
Your data for the gender_diff column currently consists of negative and positive values, which depend on which group of people (women or men) have a higher percentage. You want to find the five departments with the most balanced gender ratios, but first you decide to make your life easier by replacing the values in the gender_diff column with their respective absolute values.
##### Instructions
- Use numpy and pandas to convert each value in the gender_diff column to its absolute value.
- Output the five departments with the most balanced gender ratios.

##### Script.py
```python
#Make all gender difference values positive
recent_grads['gender_diff'] = np.abs(recent_grads['gender_diff'])

#Find the 5 rows with lowest gender rate difference
print(recent_grads.nsmallest(5, 'gender_diff'))
```

#### Exercise
##### Filtering rows
Finally you can filter out for departments which fail the benchmark of a difference of more than 0.30. Since all the values are now positive, you can do this with a simple boolean operator.

You want to find the rows containing departments that are skewed heavily towards men. Using work you've already done, you'll create a new DataFrame that contains this information.

The DataFrame recent_grads still has the columns sharemen and gender_diff that you created in previous exercises.
##### Instructions
- Create diff_30, a boolean Series that is True when the corresponding value of gender_diff is greater than 0.30 and False otherwise.
- Make another boolean Series called more_men that's true when the corresponding row in recent_grads has more men than women.
- Combine your two Series to make one that you can use to select rows that have both more men than women and a value of gender_diff greater than 0.30. Save the result as more_men_and_diff_30.
- Use this new boolean Series to create the DataFrame fewer_women that contains only the rows you're interested in.

##### Script.py
```python
#Rows where gender rate difference is greater than .30 
diff_30 = recent_grads['gender_diff'] > .30

#Rows with more men
more_men = recent_grads['sharemen'] > recent_grads['sharewomen']

#Combine more_men and diff_30
more_men_and_diff_30 = np.logical_and(more_men, diff_30)

#Find rows with more men and and gender rate difference greater than .30
fewer_women = recent_grads[more_men_and_diff_30]
```

#### Exercise

##### Grouping with Counts

There are various department categories but no sense of how many departments there are in each category. You'll use `pandas` to gain insight into this information.

In particular, you'll use the `.groupby()` method of `pandas`. This was not introduced to you in the course, but you'll see it very frequently in your data science journey and it's an important method to understand. This set of exercises will extend your `pandas` knowledge by teaching you how to use the `.groupby()` method.

Calls to `.groupby()` have the following three components: the column you want to group, the column you want to aggregate, and the statistic you want to aggregate by. For example, in our dataset, if we wanted to see the percentage of women (`'sharewomen'`) per `'major_category'`, we could leverage a `.groupby` like so: `recent_grads.groupby('major_category')['sharewomen'].mean()`. Here, we are grouping by `'major_category'`, and aggregating `'sharewomen'` by the mean. Give it a try in the IPython Shell if you're curious to see the result!

##### Instructions

Using the `.groupby()` method, group the `recent_grads` DataFrame by `'major_category'` and then count the number of departments per category using `.count()`.

##### Script.py
```python
#Group by major category and count
print(recent_grads.groupby(['major_category']).major_category.count())
```

#### Exercise

##### Grouping with Counts, Part 2

You want to get a sense of the number of majors with a lot less women, so you'll perform a similar operation as the one from the last exercise.

Use the `fewer_women` DataFrame from a previous exercise.

##### Instructions

Create a DataFrame that groups the departments by major category and shows the number of departments that are skewed in women.

##### Script.py
```python
#Group departments that have less women by category and count
print(fewer_women.groupby(['major_category']).major_category.count())
```

#### Exercise
##### Grouping One Column with Means
Similar to the exercise you just completed, you can group rows to output the means of different groups within a column.

The column gender_diff is still available in the recent_grads DataFrame.
##### Instructions
Write code that outputs the average gender percentage difference by major category.
##### Script.py
```python
#Report average gender difference by major category
print(recent_grads.groupby(['major_category']).gender_diff.mean())
```

#### Exercise

##### Grouping Two Columns with Means

You can expand the previous operation to include two columns and output the means for each. To accomplish this, modify the code you just wrote.

##### Instructions

Write a query that outputs the mean number of 'low_wage_jobs' and average 'unemployment_rate' grouped by 'major_category'.

##### Script.py

```python
#Find average number of low wage jobs and unemployment rate of each major category
dept_stats = recent_grads.groupby(['major_category'])['low_wage_jobs', 'unemployment_rate'].mean()
print(dept_stats)
```

