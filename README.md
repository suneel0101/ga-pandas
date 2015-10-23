# Objectives
Students will be able to use pandas to
- perform data analysis
- read in CSV data
- perform data munging and cleaning on dirty data
- apply advanced pandas techniques such as grouping, aggregation and pivot tables

# Agenda
0. Set up programming environment
1. Python Warm Up
2. Review of Basic Python
3. Using Other Libraries
4. Intro to Pandas
5. Wrap up & Closing thoughts

# Set Up Programming Environment (10)
## Download and Installation
Go through these steps on your own computer, but do so in collaboration with your neighbor.

0. Download and install anaconda (before class) [here](http://continuum.io/downloads).
1. Open Terminal
2. Run this command to create our development environment: `conda create -n pds pandas matplotlib ipython ipython-notebook scikit-learn` (This may take a few minutes)
3. Run this command to activate that environment: `source activate pds`
4. Run this command to open iPython notebook: `ipython notebook`

### Exercise: Getting Familiar with iPython Notebook
Run the following code in iPython notebook by typing it into a cell and pressing either the Play button or Shift+Enter to execute.

```python
print "Hello"
```

# An Exercise in Documentation (20)
What is a library? A reusable, collection of code that someone else (or you) has already written. Some great built-in libraries:
- `random`
- `csv`
- `collections`
- `datetime`

To use other libraries, we need to be able to:
- understand the documentation of that library
- understand what the inputs and outputs of their functions are
- how to call those functions correctly

Let's start with the random library.

## The `random` library.
Our first step is to locate the documentation. Google "python random". It should take you [here](https://docs.python.org/2/library/random.html)

Let's import the library
```python
>>> import random
>>> dir(random)
```

How does python know what `random` is and how to find the code? Because it comes built-in to the Python language. Other libraries such as `pandas` will have to be installed prior to use.

### Exercise 1
Find the `randint` function in the documentation and explain to your neighbor what it does and how to use it.

### Exercise 2
Again, with your partner, use the `randint` function to generate a random number between 1 and 125.

### Exercise 3
This time solo, use the `shuffle` function on this list: `[1, 2, 7, 5, 9, 10]`. What gets returned?

## What is `as`?
```python
>>> import random as rd
```

Let's see what happens...

# Intro to Pandas (45)
What is [pandas](http://pandas.pydata.org/pandas-docs/stable/)?

- analyze tabular data
- built on top of `scipy` and `numpy`, so quite fast and it's good to know some of the basics of those libraries as well since you'll likely use some function calls and have to interact with numpy arrays which are fancy, scalable lists.
- incredibly powerful

## Our First DataSet
[Here](https://s3.amazonaws.com/python-level-2/sales-funnel.csv) is the data set.

### Exercise
With your partner, download the data and look at it in excel.

Questions:
- What is this dataset about?
- What are some questions you might ask about the data?

### Importing pandas
```python
>>> import pandas as pd
```

### Exercise (55)
We want to read in the csv file. With your partner, look in the pandas documentation (or Google) to find out how to read in a csv file given a URL.
Then, read in the csv file from the above URL.

*Note*: We're going to be heavily commenting our code so that each step is super clear and we can refer back to it in the future and immediately understand what's being done.

### Basic manipulation
```python
# We've already read in csv data and saved it to a DataFrame called df
# Let's see the columns
>>> df.columns
# Let's only see the first 5 rows
>>> df[:5]
# Let's only look at Name and Status
>>> df[["Name", "Status"]]
# Let's look at just Name
>>> df["Name"]
```
### DataFrame vs DataSeries
```python
>>> type(df)
>>> df["Name"]
# just pass in the string "Name" in brackets
# and we get a Series (1-dimensional)
>>> type(df["Name"])
# instead if you pass in the list ["Name"] in the brackets
# we get a 2-dimensional DataFrame
>>> type(df[["Name"]])
```

### Questions (75)

#### Filtering dataframes
Let's learn how to filter the data according to some criterion.
- How many accounts have been won?

Exercise:
- Solo: How many accounts have a price greater than $12,000?
- Solo: just the subset of data where status is pending

#### Getting the max value (and similar quantities) (210)
What is the maximum account price?

Exercise:
- Solo: What is the minimum account price?
- Solo: What is the mean account price?
- Solo: What is the sum of all the prices?


#### Aggregating (90)
- What is the total dollar amount pending?

Step:
1. add a column called Amount that is Quantity times Price
2. select the subtable where status is pending
2. sum up the filtered amounts in that subtable

#### Pivot table basics (105)
Pivot tables are a great tool to summarize the dataset. Same concept as in Excel. Let's try it out

First, let's take a look at the documentation [here](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.pivot_table.html).

```python
>>> pd.pivot_table(df, index=["Name"])
>>> pd.pivot_table(df,index=["Manager","Rep"])
>>> pd.pivot_table(df,index=["Manager","Rep"],values=["Price"])
# Is the price column correct?
# import the numpy library to us the sum function
>>> import numpy as np
>>> pd.pivot_table(df,index=["Manager","Rep"],values=["Price"],aggfunc=np.sum)
```
Exercise:
- With partner: create a pivot table that indexes on Manager and Status and displays only the column Price, which contains the total price of accounts for each (Manager, Status) pair.
- Solo: create a pivot table indexing on Status and displays only the column Price summed up per status.

# More Pandas (120)
Let's expand our Pandas knowledge and practice it with another dataset.

Download [this dataset](https://s3-us-west-2.amazonaws.com/ga-dat-2015-suneel/rock.csv)

## Preliminary Exercise
1. Take 2 minutes to download this dataset and examine it.
2. Take 4 minutes to talk with a partner about the dataset and what kinds of insights you might extract from the data.
3. Share with the class.

## Exercises (125)
1. Read in the dataset from the url
2. Solo: How many songs were released in 1981
3. What is the earliest release year in the data (Hint: there might be dirty data...)

## Data munging (135)
### Using `.apply()` to clean up the year.
Let's create a new column that contains the clean year

### lambda functions (150)
Sometimes the data manipulation we'll want to do on a column will be pretty simple, so we can apply it in place. Say for example we wanted to lowercase an entire column (code in the iPython notebook)

#### lambda function exercises
1. Create a new column called "contains_Rock" and the value should be True if the title contains the word "Rock" and False otherwise
2. Create a new column called "contains_rock" and the value should be True if the title contains "rock" regardless of case (so it could contain "Rock", "ROCK", "roCK", etc) and False otherwise

## Using `value_counts` (175)
Pull up the pandas value_counts documentation.
We'll answer the following: What are the top 20 songs by play count?

## Using `groupby` (180)
Pull up the Pandas `groupby` documentation.
We'll look at play count grouped by artist.

# Even More Pandas (190)
Let's look at this crunchbase data.

## Preliminary Exercises
1. Read in the data.
2. Anything interesting/strange about the column names?
3. Let's rename the column names accordingly.

## Using `.describe()` to get some descriptive statistics (200)
Pull up the pandas DataFrame `describe` documentation.

## Using `.query()`
We can use boolean expressions to query the data.

Here are some examples:

### Exercises (210)
1.
2.
3.
4.
5.
6.

# Next Steps
- pandas tutorials
-


# Sources
- http://pbpython.com/pandas-pivot-table-explained.html