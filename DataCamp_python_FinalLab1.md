# Microsoft DataCamp

## Introduction to Python for Data Science_Final Lab

### Section 1

#### Exercise

##### Read and explore your data

In this lab, you'll explore a dataset containing information on a university's recent graduates for each department. The URL this dataset can be downloaded from is stored in a variable called `recent_grads_url`. In this exercise, you'll read in this data using Python's `pandas` module.

##### Instructions 

- Import `pandas` as `pd`.
- Read in the data from `recent_grads_url` (which is a CSV file) and assign it to a variable called `recent_grads`.
- Print the `shape` of `recent_grads`.

##### Script.py

```python
#Import pandas 
import pandas as pd

#Use pandas to read in recent_grads_url
recent_grads =pd.read_csv(recent_grads_url)

#Print the shape
print(recent_grads.shape)
```

#### Exercise

##### Exploring Your Data

Now you'll perform some data exploration using the Python `pandas`module. To get a sense of the data, you'll output statistics such as mean, median, count, and percentiles.

The DataFrame `recent_grads` is still in your workspace.

##### Instructions
- Print the .dtypes of your data so that you know what each column contains.
- Output basic summary statistics using a single pandas function.
- With the same function from before, summary statistics for all columns that aren't of type object.

##### Script.py
```python
#Print .dtypes
print(recent_grads.dtypes)

#Output summary statistics
print(recent_grads.describe())

#Exclude data of type object
print(recent_grads.describe(exclude=["object"]))
```

#### Exercise
##### Replacing Missing Values
There are some missing values in the dataset that are coded as a string. You'll update these to a value that Python understands as "missing."

The list columns contains the names of the columns you'll be working with in this exercise.
##### Instructions
- Look at the dtypes of the columns in columns to make sure that the data is numeric.
- It looks like a string is being used to encode missing values. Use the .unique() method to figure out what the string is.
- Search for missing values in the median, p25th, and p75th columns.
- Replace the found missing values with a NaN value, using numpy's np.nan.

##### Script.py
```python
#Names of the columns we're searching for missing values 
columns = ['median', 'p25th', 'p75th']

#Take a look at the dtypes
print(recent_grads[columns].dtypes)

#Find how missing values are represented
print(recent_grads["median"].unique())

#Replace missing values with NaN
for column in columns:
    recent_grads.loc[recent_grads[column]== 'UN', column] = np.nan
```

#### Exercise

##### Select a Column
Python's pandas module allows you to select a specific column from a DataFrame, which is especially useful for when you only need to manipulate one piece of data. In this exercise, you'll select the sharewomen column, which shows the percentage of women for a given department.

The DataFrame recent_grads is still in your workspace.

##### Instructions
- Select the sharewomen column from recent_grads and assign this to a variable named sw_col.
- Output the first 5 rows of sw_col.

##### Script.py
```python
#Select sharewomen column
sw_col = recent_grads.sharewomen

#Output first five rows
print(sw_col.head())
```

#### Exercise
##### Column Maximum Value
Now that you've selected the sharewomen column, you'll use numpy to output its maximum value.

The variable sw_col you created in the last exercise is still available in your workspace.
##### Instructions
- Import numpy as np.
- Using a numpy built-in function, find the maximum value of the sharewomen column and assign this value to the variable max_sw.
- Print the value of max_sw

##### Script.py
```python
#Import numpy
import numpy as np

#Use max to output maximum values
max_sw = np.amax(sw_col)

#Print column max
print(max_sw)
```

#### Exercise
##### Selecting a Row
While you know what the maximum percentage of women in a department is, which department is this? You'll output this information by filtering the dataset with pandas.

The variables sw_col and max_sw are still in your workspace.
##### Instructions
Output the row of data for the department that has the largest percentage of women.

##### Script.py
```python
#Output the row containing the maximum percentage of women
print(recent_grads[sw_col == max_sw])
```

#### Exercise
##### Converting a DataFrame to Numpy Array
Since numpy is such a powerful Python module, this exercise asks you to convert a pandas DataFrame to a numpy array to then utilize a statistics metric available through numpy in the next exercise.
##### Instructions
- Select the columns unemployed and low_wage_jobs from recent_grads, then convert them to a numpy array. Save this as recent_grads_np.
- Print the type of recent_grads_np to see that it is a numpy array.

##### Script.py
```python
#Convert to numpy array
recent_grads_np = recent_grads[["unemployed","low_wage_jobs"]].values

#Print the type of recent_grads_np
print(type(recent_grads_np))
```

#### Exercise
##### Correlation Coefficient
You have some suspicion that there's a relationship between the low_wage_jobs and unemployment_rate columns, so you decide to use numpy to calculate the correlation coefficient.
##### Instructions
Calculate the correlation matrix of the numpy array recent_grads_np.

##### Script.py
```python
print(np.corrcoef(recent_grads_np[:,0], recent_grads_np[:,1]))
```
