# Objectives
The primary goal is to get the students comfortable enough with `pandas` to apply it to their data processing and analysis tasks.

Students will be able to use `pandas` to
- perform data analysis
- read in CSV data
- perform data munging and cleaning on dirty data
- apply advanced pandas techniques such as grouping, aggregation and pivot tables

# Agenda
0. Set up programming environment
1. Python Warm Up
2. Using Documentation
3. Go Deep into Pandas
4. Wrap Up & Next Steps

# Setup
1. Go to [tmpnb.org](http://tmpnb.org).
2. Select `New` > `Python 2` to create a Python notebook.
3. Follow along with me:

```python
>>> import pandas
>>> import sklearn
>>> import matplotlib
```
**Caveat**: Don't hard refresh otherwise you'll lose your code.
*Note*: to execute a cell, run Shift + Enter


# Python Warm-Up / Review (20)
This problem will give us a review of lists, for loops and lambda functions

Given the following list,

```
names = ["Michael Fassbender", "Karlie Kloss", "Taylor Swift", "Justin Bieber"]

```
1. print out the names that contain the letter "l"
2. turn all of the names lowercase
3. sort the list of names alphabetically using the built-in `sorted` function (HINT: Use Google)
4. sort the list of names by length using the built-in `sorted` function


# Warming Up to Documentation (20)
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

### Exercises
1. Find the `randint` function in the documentation and explain to your neighbor what it does and how to use it.
2. Again, with your partner, use the `randint` function to generate a random number between 1 and 125.

## What is `as`?

Let's see what happens:
```python
>>> import random as rd
>>> random.randint
>>> rd.randint
```

# Pandas (65)
*Question* What is [`pandas`](http://pandas.pydata.org/pandas-docs/stable/)?

[Here](https://s3.amazonaws.com/python-level-2/sales-funnel.csv) is our first data set. Let's download it and upload it to the datasets folder within the notebook.

## Preliminary Exercise
With your partner
0. Download and open the dataset
1. What is this dataset about?
2. What are some questions you might ask about the data?

## Basic Manipulation (75)
0. Let's read in the data.
0. How do we see what columns are available?
1. How do we look at just the head or tail of the dataset?
2. How do we look at only a few rows?
3. How do we only look at certain columns?
4. How do we pull out a column and look at it as a series?

## Filtering DataFrames (80)
0. How do we look at only those rows that have Status = won
1. Exercise: How many accounts have a price greater than $12,000?
2. How do we get the maximum value of a certain column?
3. Exercise: What is the minimum account price? The mean? The sum? The standard deviation?

## Aggregating data (120)
What is the total dollar amount pending?

0. How do we add columns?
1. Let's add a column called Amount that is equal to Quantity * Price
2. Exercise: Let's select just those rows where status is pending and sum up those amounts.

## Pivot tables (130)
*Question*: What are pivot tables? Why are they useful?

Let's take a look at the documentation [here](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.pivot_table.html).

0. Let's pivot using one index.
1. Let's pivot on multiple indexes
2. Let's reverse those indexes
3. Let's specify which values we care about
4. Let's specify which columns we want broken down
5. Let's specify how we want the values to be aggregated (`aggfunc`)
6. Let's fill N/A values
7. Let's get subtotals

(Creative) Exercise: with a partner, use pivot tables to play around with the data. What pivots do you find particularly interesting or useful for this dataset?

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
Sometimes the data manipulation we'll want to do on a column will be pretty simple, so we can apply it in place. Say for example we wanted to lowercase an entire column

```python
>>> df["lowercase_title"] = df["Song Clean"].apply(lambda val: val.lower())
```

#### lambda function exercises
1. Create a new column called "contains_Rock" and the value should be True if the title contains the word "Rock" and False otherwise
2. Create a new column called "contains_rock" and the value should be True if the title contains "rock" regardless of case (so it could contain "Rock", "ROCK", "roCK", etc) and False otherwise

## Using `value_counts` (175)
Pull up the pandas value_counts documentation.
We'll answer the following: What are the top 20 songs by play count?

```python
>>> df["ARTIST CLEAN"].value_counts()[:20]
```
## Using `groupby` (180)
Pull up the Pandas `groupby` documentation.
We'll look at play count grouped by artist.

```python
>>> df.groupby("ARTIST CLEAN")["PlayCount"].mean()
```

# Even More Pandas (190)
Let's look at [this dataset](https://raw.githubusercontent.com/suneel0101/lesson-plan/master/crunchbase_monthly_export.csv) from Crunchbase

## Preliminary Exercises
1. Solo: Read in the data. What is this data about? What are some questions you want to answer about the data?
2. What is the max funding total?
3. Partner: Anything interesting/strange about the column names?
4. Class altogether: Let's rename the column names accordingly.

## Using `.describe()` to get some descriptive statistics
Pull up the pandas DataFrame `describe` documentation.

## Exercises (200)

1. Construct a pivot table that indexes on region and shows the total funding amounts by region
2. What is the average number of funding rounds for companies in NYC? How does that compare to SF?
3. What are the top 3 markets with the highest average funding total per company?
4. How many companies have Games as a category? What's their average funding total? Using a pivot table, what's the average funding total of those companies that have Games as a category, broken down by Region?
5. What is the most popular category of company?

# Sharing Our Analysis
1. Download the iPython notebook
2. Paste it into a [GitHub gist](http://gist.github.com)
3. Copy the URL of the gist and paste it [here](http://nbviewer.ipython.org)
4. Voilà, now you have a shareable analysis!

# Next Steps
To continue your Python/Pandas/Data Science education, recommend the following:
- [pandas tutorials](http://pandas.pydata.org/pandas-docs/stable/tutorials.html)
- [GA's part-time data science course](https://generalassemb.ly/education/data-science)