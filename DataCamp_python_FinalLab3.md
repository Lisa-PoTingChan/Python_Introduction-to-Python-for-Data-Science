# Microsoft DataCamp

## Introduction to Python for Data Science_Final Lab

### Section 3

#### Exercise

##### Plotting Scatterplots

Now that you've calculated the correlation coefficient between the `low_wage_jobs` and `unemployment_rate` columns, you want to create a visualization to effectively display this relationship. You'll use `matplotlib` to create a scatterplot of these two columns.

The DataFrame `dept_stats` is available in your workspace again, and the columns `low_wage_jobs` and `unemployment_rate` have been extracted into variables of the same name.

##### Instructions

- Import matplotlib.pyplot with the alias plt.

- Create a scatter plot between unemployment_rate and low_wage_jobs per major category.
- Label the x axis with 'Unemployment rate'.
- Label the y axis with 'Low pay jobs'.

##### Script.py
```python
# Import matplotlib
import matplotlib.pyplot as plt

# Create scatter plot
plt.scatter(unemployment_rate,low_wage_jobs)

# Label x axis
plt.xlabel('Unemployment rate')

# Label y axis
plt.ylabel('Low pay jobs')

# Display the graph 
plt.show()
```

#### Exercise

##### Modifying Plot Colors

The default settings for `matplotlib` may not be what you hope to present to others, so you decide to customize your plot for low wages versus unemployment rate.

Use the `pandas` DataFrame `dept_stats` again.

##### Instructions

- Create the scatterplot visualization between the unemployment rate and number of low wage jobs per major category using the `.plot()`method.
- Customize this scatterplot so that the points are red triangles by setting the `color` argument to `"r"` and the `marker` argument `^`.
- Display the plot you've created!

##### Script.py

```python
# Plot the red and triangle shaped scatter plot  
plt.scatter(unemployment_rate,low_wage_jobs, color="r", marker="^")

# Display the visualization
plt.show()
```

#### Exercise

##### Plotting Histograms

Now that you've taken a look at that scatterplot, you want to go back to the `sharewomen` column that you were working with earlier. Specifically, you want to get an idea of how the values of `sharewomen` are distributed. This means you want to plot a histogram. For your convenience, the `sharewomen` column has been extracted from the `recent_grads`DataFrame into a variable called `sharewomen`.

##### Instructions

- Use `matplotlib` to create a histogram of `sharewomen`.
- Show the plot you created.


##### Script.py
```python
# Plot a histogram of sharewomen
plt.hist(sharewomen)

# Show the plot
plt.show()
```

#### Exercise

##### Plotting with pandas

In Python, there are several different ways to create visualizations. In fact, `pandas` has its own visualization capabilities, all of which are built on top of `matplotlib`! For example, you could have created the histogram from the previous exercise using `recent_grads.sharewomen(kind="hist")` instead of `plt.hist(recent_grads.sharewomen)`.

Which approach you prefer comes down to personal preference - when working with DataFrames, it is advantageous to use `pandas`' plotting capabilities because the code tends to be less verbose.

Here, you will practice creating the plots from the previous exercises using `pandas` instead of `matplotlib`. All `pandas` plots are created using the `.plot()` method on a DataFrame. Inside `.plot()`, you can specify which plot you want to create using the `kind` parameter. For example, `kind= 'hist'` would create a histogram, `kind='scatter'`would create a scatter plot, and so on.

##### Instructions

1. Use the `.plot()` method with `kind='scatter'` on the `dept_stats`DataFrame to create a scatter plot with `'unemployment_rate'` on the x-axis and `'low_wage_jobs'` on the y-axis. 
2. Now, create a histogram of the `sharewomen` column of the `recent_grads` DataFrame. 


##### Script.py
```python
# Import matplotlib and pandas
import matplotlib.pyplot as plt
import pandas as pd

# Create scatter plot
dept_stats.plot(kind='scatter', x='unemployment_rate', y='low_wage_jobs')
plt.show()

# Create histogram
recent_grads.sharewomen.plot(kind='hist')
plt.show()
```

#### Exercise

##### Plotting One Bar Graphs

Next, you want to gauge how many students are graduating from each major category without a job that requires their degree, so you decide to create a bar chart between number of non college jobs and each major category.

##### Instructions

- First, create a DataFrame to plot. Use `recent_grads` to make a DataFrame that reports each major category and the number of college graduates with a job that doesn't require a degree. Assign this to a variable named `df`.
- Plot this data as a bar chart using the `.plot()` method. Here, `kind`should be `"bar"`.
- Display the plot you've created!


##### Script.py
```python
# DataFrame of non-college job sums
df = recent_grads.groupby(['major_category']).non_college_jobs.sum()

# Plot bar chart
df.plot(kind='bar')

# Show graph
plt.show()
```

#### Exercise

##### Plotting Two Bar Graphs

The previous visualization gives you a good picture of how many students are working at jobs that don't require a college degree, but it doesn't give you a sense of how each category is doing relative to one another. So you decide to add the `college_jobs` column as an extra bar of information so that you can evaluate the difference between the two.

##### Instructions

- Use `pandas` to create a DataFrame that reports the number of graduates working at jobs that do require college degrees (`'college_jobs'`), and do not require college degrees (`'non_college_jobs'`). Assign this to a variable named `df1`.
- Create a plot that reports this data with `matplotlib`.
- Display the plot you've created!


##### Script.py
```python
# DataFrame of college and non-college job sums
df1 = recent_grads.groupby(['major_category'])['college_jobs','non_college_jobs'].sum()

# Plot bar chart
df1.plot(kind="bar")

# Show graph
plt.show()
```

#### Exercise

##### Dropping Missing Values

Now that you've replaced the `UN` values with `NaN` values, you realize it's better that you just delete these rows completely. In this exercise, you'll do just that. To confirm you filtered out the rows, you’ll then check the size of the DataFrame to confirm the size is smaller.

##### Instructions

- With a single line of code, drop all the rows that have a missing value.
- Print the size of the manipulated DataFrame.


##### Script.py
```python
# Print the size of the DataFrame
print(recent_grads.size)

# Drop all rows with a missing value
recent_grads.dropna(axis = 0, inplace = True)

# Print the size of the DataFrame
print(recent_grads.size)
```

#### Exercise

##### Plotting Quantiles of Salary, Part 1

Now you're interested in plotting a few different quantiles of the average salary across major categories so that you can compare the different distributions of salary. In this exercise you'll prepare your data for `matplotlib`.

##### Instructions

- The columns `median`, `p25th`, and `p75th` are currently encoded as strings. Convert these columns to numerical values. Then, divide the value of each column by 1000 to make the scale of the final plot easier to read.
- Find the of each of the three columns for each major category. Save this as `sal_quantiles`


##### Script.py
```python
# Convert to numeric and divide by 1000
recent_grads['median'] = pd.to_numeric(recent_grads['median']) / 1000
recent_grads['p25th'] = pd.to_numeric(recent_grads['p25th']) / 1000
recent_grads['p75th'] = pd.to_numeric(recent_grads['p75th']) / 1000

# Select averages by major category
columns = ['median', 'p25th', 'p75th']
sal_quantiles = recent_grads.groupby(['major_category'])[columns].mean()
```

#### Exercise

##### Plotting Quantiles of Salary, Part 2

Now that your data is ready for plotting, it's time to make the final plot!

##### Instructions

- Plot the DataFrame.
- Clean up the x-axis labels with the function `plt.xticks()`. Set the first argument equal to `np.arange(len(sal_quantiles.index))`, the second argument equal to `sal_quantiles.index`, and the keyword argument `rotation = 'vertical'`.
- Show the plot.
- Now call the `.plot()` method with the argument `subplots=True` to plot the columns on separate axes. Show this plot as well.


##### Script.py
```python
# Plot the data
sal_quantiles.plot()

# Set xticks
plt.xticks(
    np.arange(len(sal_quantiles.index)),
    sal_quantiles.index, 
    rotation='vertical')

# Show the plot
plt.show()

# Plot with subplots
sal_quantiles.plot(subplots=True)
plt.show()
```

