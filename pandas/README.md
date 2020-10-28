# Pandas

References:

https://www.kaggle.com/learn/pandas
https://www.kaggle.com/python10pm/pandas-75-exercises-with-solutions
https://www.kaggle.com/python10pm/pandas-100-tricks

## Getting started
To use pandas, you'll typically start with the following line of code.

```python
import pandas as pd
```

## Creating data

### DataFrame
A DataFrame is a table. It contains an array of individual entries, each of which has a certain value. Each entry corresponds to a row (or record) and a column.

```python
# Create a dataframe with incremnetal integer index
pd.DataFrame({'Yes': [50, 21], 'No': [131, 2]})

# Create a dataframe with defined sting index
pd.DataFrame(
    {'Bob': ['I liked it.', 'It was awful.'], 'Sue': ['Pretty good.', 'Bland.']},
    index=['Product A', 'Product B']
)
```

## Reading data files
Being able to create a DataFrame or Series by hand is handy. But, most of the time, we won't actually be creating our own data by hand. Instead, we'll be working with data that already exists.

Data can be stored in any of a number of different forms and formats. By far the most basic of these is the humble CSV file.

So a CSV file is a table of values separated by commas. Hence the name: "Comma-Separated Values", or CSV.

Let's now set aside our toy datasets and see what a real dataset looks like when we read it into a DataFrame. We'll use the `pd.read_csv()` function to read the data into a DataFrame. We can use the shape attribute to check how large the resulting DataFrame is.

```python
# Read a .csv file and store in variable
wine_reviews = pd.read_csv("../input/wine-reviews/winemag-data-130k-v2.csv")
# We can check the shape of dataframe by .shape attribute with (rows, columns)
wine_reviews.shape  # In this case returns (129971, 14)
```

We can examine the contents of the resultant DataFrame using the `.head(n=5)` command, which grabs the first five rows:

```python
wine_reviews.head()  # Returns a view of top 5 entries of dataframe
```

## Indexing

In Python, we can **access the property of an object by accessing it as an attribute**. A **book** object, for example, might have a **title property**, which we can access by calling `book.title` or `book['title']`. Columns in a pandas DataFrame work in much the same way.

To drill down to a single specific value, we need only use the indexing operator `[]`. For example: `book['title'][0]` will return the first title.

### Indexing in pandas
The indexing operator and attribute selection are nice because they work just like they do in the rest of the Python ecosystem. As a novice, this makes them easy to pick up and use. However, pandas has its own accessor operators, loc and iloc. For more advanced operations, these are the ones you're supposed to be using.

#### Index-based selection
Pandas indexing works in one of two paradigms. The first is **index-based selection**: selecting data based on its numerical position in the data. `iloc` follows this paradigm.

To select the **first row of data** in a DataFrame, we may use the following:

```python
book.iloc[0]  # Returns the first row of the dataframe named book
```

Both loc and iloc are **row-first, column-second**. This is the opposite of what we do in native Python, which is column-first, row-second.

This means that it's marginally easier to retrieve rows, and marginally harder to get retrieve columns. To get a column with iloc, we can do the following:

```python
reviews.iloc[:, 0]  # Retuns the first column (all row entries and column 0)
```

On its own, the : operator, which also comes from native Python, means "everything". When combined with other selectors, however, it can be used to **indicate a range** of values. Or it's also possible to **pass a list**.


#### Label-based selection
The second paradigm for attribute selection is the one followed by the `loc` operator: label-based selection. In this paradigm, it's the **data index value**, not its position, which matters.

For example, to get the first title entry in book, we would now do the following:

```python
book.loc[0, 'title']  # Returns the first entry for column named title
book.loc[:, ['title', 'score', 'comments']]  # Returns all rows for selected named columns
```

### Manipulating the index
Label-based selection derives its power from the labels in the index. Critically, the index we use is not immutable. We can manipulate the index in any way we see fit.

The `set_index()` method can be used to do the job.


## Selecting

### Conditional selection
So far we've been indexing various strides of data, using structural properties of the DataFrame itself. To do interesting things with the data, however, we often need to ask questions based on conditions.

For example, suppose that we're interested specifically in better-than-average books produced in Italy.

We can start by checking if each book is Italian or not:

```python
book.country == 'Italy'  # True o False if each entry of book, it's country is equal to Italy (length = book rows)
```

This operation produced a Series of True/False booleans based on the country of each record. This result can then be used inside of loc to select the relevant data:

```python
book.loc[book.country == 'Italy']  # Returns a dataframe where all book countries are 'Italy'
```

We can use the ampersand`&` to bring two questions together. To create or statement wi will use `|`.

```python
book.loc[(book.country == 'Italy') & (book.score >= 90)]  # Returns a dataframe where all book countries are 'Italy' AND score >= 90
book.loc[(book.country == 'Italy') | (book.score >= 90)]  # Returns a dataframe where all book countries are 'Italy' OR score >= 90
```

Pandas comes with a few built-in conditional selectors, two of which we will highlight here.

`isin` is lets you select data whose value "is in" a list of values. For example, here's how we can use it to select books only from Italy or France:

```python
book.loc[book.country.isin(['Italy', 'France'])]  # Return dataframe of books from 'Italy' or 'France'
```

The second is `isnull` (and its companion `notnull`). These methods let you highlight values which are (or are not) empty (NaN).

```python
book.loc[book.price.notnull()]  # Returns dataframe with books where price is NOT null
book.loc[book.price.isnull()]  # Returns dataframe with books where price IS null
```


## Assigning
### Assigning data
Going the other way, assigning data, or creating a new column, to a DataFrame is easy. 

```python
book['critic'] = 'everyone'  # Creates a column 'critic' with values 'everyone'
book['index_backwards'] = range(len(book), 0, -1)  # Create a column with descending from len(book) to 0 by steps of -1
```

## Summary functions

Pandas provides many simple "summary functions" (not an official name) which restructure the data in some useful way. For example, `describe()` generates a high-level summary of the attributes of the given column. It is type-aware, meaning that its **output changes based on the data type** of the input.

If you want to get some particular simple summary statistic about a column in a DataFrame or a Series, there is usually a helpful pandas function that makes it happen.

  - my_dataframe.my_column.**mean()**: Mean of the entries of selected column
  - my_dataframe.my_column.**unique()**: Unique values of selected column
  - my_dataframe.my_column.**value_counts()**: List of unique values and how often they occur in the dataset of selected column.

## Maps
A map is a term, borrowed from mathematics, for a function that **takes one set of values and "maps" them to another** set of values. In data science we often have a need for creating new representations from existing data, or for transforming data from the format it is in now to the format that we want it to be in later. Maps are what handle this work, making them extremely important for getting your work done!

There are two mapping methods that you will use often.

`map()` is the first, and slightly simpler one. For example, suppose that we wanted to remean the scores the book received to 0. We can do this as follows:

```python
book_score_mean = book.score.mean()  # Get scores column mean value
book.score.map(lambda p: p - book_score_mean)  # Define the score column as his values - mean value 
```

The function you pass to map() should expect a single value from the Series (a point value, in the above example), and return a transformed version of that value. map() returns a new Series where all the values have been transformed by your function.

`apply() is the equivalent method if we want to transform a whole DataFrame by **calling a custom method on each row**.

```python
book_score_mean = book.score.mean()  # Get scores column mean value

def remean_scores(row):
    # Define the score column as his values - mean value 
    row.score = row.score - book_score_mean
    return row

book.apply(remean_scores, axis='columns')  # Call to remean_scores()
```

If we had called book.apply() **with axis='index'**, then instead of passing a function to transform each row, we would need to give a function to **transform each column**.

**Note** that map() and apply() return new, transformed Series and DataFrames, respectively. **They don't modify the original data they're called on**. If we look at the first row of book, we can see that it still has its original score value.

## Grouping 

One function we've been using heavily thus far is the value_counts() function. We can replicate what value_counts() does by doing the following:

```python
book.groupby('score').score.count()  # Return the count of grouped scores
```

`groupby()` created a group of books which allotted the same score values to the given book. Then, for each of these groups, we grabbed the scores() column and counted how many times it appeared. value_counts() is just a shortcut to this groupby() operation.

We can use any of the summary functions we've used before with this data. For example, to get the cheapest book in each score value category, we can do the following:

```python
book.groupby('score').price.min()  # Returns a series os score - cheapest prices
```

You can think of each group we generate as being a slice of our DataFrame containing only data with values that match. This DataFrame is accessible to us directly using the apply() method, and we can then manipulate the data in any way we see fit.

```python
book.groupby('score').apply(lambda df: df.title.iloc[0])  # Returns a series of score - first book with that score
```

Another groupby() method worth mentioning is `agg()`, which lets you run a bunch of different functions on your DataFrame simultaneously. For example, we can generate a simple statistical summary of the dataset as follows:

```python
book.groupby(['country']).price.agg([len, min, max])  # Returns the len, min and max prices of books per country 
```

### Multi-indexes
In all of the examples we've seen thus far we've been working with DataFrame or Series objects with a single-label index. groupby() is slightly different in the fact that, depending on the operation we run, it will sometimes result in what is called a multi-index.

A multi-index differs from a regular index in that it has multiple levels. For example:

```python
# Get a country  province - num books | One country can have multiple provinces
countries_reviewed = book.groupby(['country', 'province']).description.agg([len])
```

Multi-indices have several methods for dealing with their tiered structure which are absent for single-level indices. They also require two levels of labels to retrieve a value. Dealing with multi-index output is a common "gotcha" for users new to pandas.

The use cases for a multi-index are detailed alongside instructions on using them in the [MultiIndex / Advanced Selection](https://pandas.pydata.org/pandas-docs/stable/user_guide/advanced.html) section of the pandas documentation.

However, in general the multi-index method you will use most often is the one for converting back to a regular index, the reset_index() method:

```python
countries_reviewed.reset_index()
```

## Sorting

Looking again at countries_reviewed we can see that grouping returns data in index order, not in value order. That is to say, when outputting the result of a groupby, the order of the rows is dependent on the values in the index, not in the data.

To get data in the order want it in we can sort it ourselves. The `sort_values()` method is handy for this.

```python
countries_reviewed = countries_reviewed.reset_index()
countries_reviewed.sort_values(by='len')
```

sort_values() defaults to an ascending sort, where the lowest values go first. However, most of the time we want a descending sort, where the higher numbers go first. That goes thusly:

```python
countries_reviewed.sort_values(by='len', ascending=False)
```

To sort by index values, use the companion method sort_index(). This method has the same arguments and default order:

```python
countries_reviewed.sort_index()
```

Finally, know that you can sort by more than one column at a time:

```python
countries_reviewed.sort_values(by=['country', 'len'])
```

## Data Types

### Dtypes
The data type for a column in a DataFrame or a Series is known as the dtype.

You can use the `dtype` property to grab the type of a specific column. Alternatively, the `dtypes` property returns the dtype of every column in the DataFrame.

Data types tell us something about how pandas is storing the data internally. float64 means that it's using a 64-bit floating point number; int64 means a similarly sized integer instead, and so on.

One peculiarity to keep in mind (and on display very clearly here) is that columns consisting entirely of strings do not get their own type; they are instead given the object type.

It's possible to convert a column of one type into another wherever such a conversion makes sense by using the astype() function. For example, we may transform the scores column from its existing int64 data type into a float64 data type:

```python
book.score.astype('float64')
```

## Missing Data

Entries missing values are given the value NaN, short for "Not a Number". For technical reasons these NaN values are always of the float64 dtype.

Pandas provides some methods specific to missing data. To select NaN entries you can use `pd.isnull()` (or its companion `pd.notnull()`).

```python
book[pd.isnull(book.country)]  # Select entries without country (country == NaN)
```

Replacing missing values is a common operation. Pandas provides a really handy method for this problem: fillna(). fillna() provides a few different strategies for mitigating such data. For example, we can simply replace each NaN with an "Unknown":

```python
book.country.fillna("Unknown")  # Sets all entries without country to 'Unknown'
```

Or we could fill each missing value with the first non-null value that appears sometime after the given record in the database. This is known as the backfill strategy.

Alternatively, we may have a non-null value that we would like to replace. For example, suppose that since this dataset was published, reviewer Kerin O'Keefe has changed her Twitter handle from @kerinokeefe to @kerino. One way to reflect this in the dataset is using the replace() method:

```python
book.taster_twitter_handle.replace("@kerinokeefe", "@kerino")
```

The replace() method is worth mentioning here because it's handy for replacing missing data which is given some kind of sentinel value in the dataset: things like "Unknown", "Undisclosed", "Invalid", and so on.

## Renaming

`rename()` lets you change index names and/or column names. For example, to change the scores column in our dataset to puntuacion, we would do:

```python
book.rename(columns={'score': 'puntuacion'})
```

rename() lets you rename index or column values by specifying a index or column keyword parameter, respectively. It supports a variety of input formats, but usually a Python dictionary is the most convenient. Here is an example using it to rename some elements of the index.

```python
book.rename(index={0: 'firstEntry', 1: 'secondEntry'})  # Renames the index 0 to 'firstEntry' and 1 to 'secondEntry'
```

You'll probably rename columns very often, but rename index values very rarely. For that, set_index() is usually more convenient.

Both the row index and the column index can have their own name attribute. The complimentary `rename_axis()` method may be used to change these names.

```python
book.rename_axis("books", axis='rows').rename_axis("fields", axis='columns')
```

## Combining

When performing operations on a dataset, we will sometimes need to combine different DataFrames and/or Series in non-trivial ways. Pandas has three core methods for doing this. In order of increasing complexity, these are `concat()`, `join()`, and `merge()`. Most of what merge() can do can also be done more simply with join(), so we will omit it and focus on the first two functions here.

The simplest combining method is `concat()`. Given a list of elements, this function will smush those elements together along an axis.

This is useful when we have data in different DataFrame or Series objects but having the same fields (columns). 

```python
canadian_youtube = pd.read_csv("../input/youtube-new/CAvideos.csv")
british_youtube = pd.read_csv("../input/youtube-new/GBvideos.csv")

pd.concat([canadian_youtube, british_youtube])
```
