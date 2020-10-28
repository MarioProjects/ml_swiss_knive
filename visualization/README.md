# Data Visualization

### Set up the notebook
There are a few lines of code that you'll need to run at the top of every notebook to set up your coding environment. It's not important to understand these lines of code now, and so we won't go into the details just yet. (Notice that it returns as output: Setup Complete.)


```python
import warnings
warnings.filterwarnings('ignore')
import pandas as pd
pd.plotting.register_matplotlib_converters()
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns
```

## Line Charts


```python
# Path of the file to read
spotify_filepath = "data/spotify.csv"

# Read the file into a variable spotify_data
spotify_data = pd.read_csv(spotify_filepath, index_col="Date", parse_dates=True)

spotify_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Shape of You</th>
      <th>Despacito</th>
      <th>Something Just Like This</th>
      <th>HUMBLE.</th>
      <th>Unforgettable</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2017-01-06</th>
      <td>12287078</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-01-07</th>
      <td>13190270</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-01-08</th>
      <td>13099919</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-01-09</th>
      <td>14506351</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2017-01-10</th>
      <td>14275628</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Set the width to 14 inches and height 6 inches to the figure 
plt.figure(figsize=(14,6))

# Add title
plt.title("Daily Global Streams of Popular Songs in 2017-2018")

# Line chart showing how FIFA rankings evolved over time 
# The output is well formated as time because index col type is Date
sns.lineplot(data=spotify_data)
```




    <AxesSubplot:title={'center':'Daily Global Streams of Popular Songs in 2017-2018'}, xlabel='Date'>




    
![png](README_files/README_5_1.png)
    


### Plot a subset of the data
So far, you've learned how to plot a line for every column in the dataset. In this section, you'll learn how to plot a subset of the columns.

We'll begin by printing the names of all columns. This is done with one line of code and can be adapted for any dataset by just swapping out the name of the dataset (in this case, spotify_data).


```python
list(spotify_data.columns)
```




    ['Shape of You',
     'Despacito',
     'Something Just Like This',
     'HUMBLE.',
     'Unforgettable']



In the next code cell, we plot the lines corresponding to the first two columns in the dataset.


```python
# Set the width to 14 inches and height 6 inches to the figure 
plt.figure(figsize=(14,6))

# Add title
plt.title("Daily Global Streams of Popular Songs in 2017-2018")

# Line chart showing daily global streams of 'Shape of You'
sns.lineplot(data=spotify_data['Shape of You'], label="Shape of You")

# Line chart showing daily global streams of 'Despacito'
sns.lineplot(data=spotify_data['Despacito'], label="Despacito")

# Add label for horizontal axis
plt.xlabel("Date")
```




    Text(0.5, 0, 'Date')




    
![png](README_files/README_9_1.png)
    


## Bar Charts


```python
# Path of the file to read
flight_filepath = "data/flight_delays.csv"

# Read the file into a variable flight_data
flight_data = pd.read_csv(flight_filepath, index_col="Month")

flight_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>AA</th>
      <th>AS</th>
      <th>B6</th>
      <th>DL</th>
      <th>EV</th>
      <th>F9</th>
      <th>HA</th>
      <th>MQ</th>
      <th>NK</th>
      <th>OO</th>
      <th>UA</th>
      <th>US</th>
      <th>VX</th>
      <th>WN</th>
    </tr>
    <tr>
      <th>Month</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>6.955843</td>
      <td>-0.320888</td>
      <td>7.347281</td>
      <td>-2.043847</td>
      <td>8.537497</td>
      <td>18.357238</td>
      <td>3.512640</td>
      <td>18.164974</td>
      <td>11.398054</td>
      <td>10.889894</td>
      <td>6.352729</td>
      <td>3.107457</td>
      <td>1.420702</td>
      <td>3.389466</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7.530204</td>
      <td>-0.782923</td>
      <td>18.657673</td>
      <td>5.614745</td>
      <td>10.417236</td>
      <td>27.424179</td>
      <td>6.029967</td>
      <td>21.301627</td>
      <td>16.474466</td>
      <td>9.588895</td>
      <td>7.260662</td>
      <td>7.114455</td>
      <td>7.784410</td>
      <td>3.501363</td>
    </tr>
    <tr>
      <th>3</th>
      <td>6.693587</td>
      <td>-0.544731</td>
      <td>10.741317</td>
      <td>2.077965</td>
      <td>6.730101</td>
      <td>20.074855</td>
      <td>3.468383</td>
      <td>11.018418</td>
      <td>10.039118</td>
      <td>3.181693</td>
      <td>4.892212</td>
      <td>3.330787</td>
      <td>5.348207</td>
      <td>3.263341</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4.931778</td>
      <td>-3.009003</td>
      <td>2.780105</td>
      <td>0.083343</td>
      <td>4.821253</td>
      <td>12.640440</td>
      <td>0.011022</td>
      <td>5.131228</td>
      <td>8.766224</td>
      <td>3.223796</td>
      <td>4.376092</td>
      <td>2.660290</td>
      <td>0.995507</td>
      <td>2.996399</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5.173878</td>
      <td>-1.716398</td>
      <td>-0.709019</td>
      <td>0.149333</td>
      <td>7.724290</td>
      <td>13.007554</td>
      <td>0.826426</td>
      <td>5.466790</td>
      <td>22.397347</td>
      <td>4.141162</td>
      <td>6.827695</td>
      <td>0.681605</td>
      <td>7.102021</td>
      <td>5.680777</td>
    </tr>
  </tbody>
</table>
</div>



You may notice that the code is slightly shorter than what we used in the previous tutorial. In this case, since the row labels (from the 'Month' column) don't correspond to dates, we don't add parse_dates=True in the parentheses.

Say we'd like to create a bar chart showing the average arrival delay for Spirit Airlines (airline code: NK) flights, by month.


```python
# Set the width and height of the figure
plt.figure(figsize=(14,6))

# Add title
plt.title("Average Arrival Delay for Spirit Airlines Flights, by Month")

# Bar chart showing average arrival delay for Spirit Airlines flights by month
sns.barplot(x=flight_data.index, y=flight_data['NK'])

# Add label for vertical axis
plt.ylabel("Arrival delay (in minutes)")
```




    Text(0, 0.5, 'Arrival delay (in minutes)')




    
![png](README_files/README_14_1.png)
    


`x=flight_data.index` - This determines what to use on the horizontal axis. In this case, we have selected the column that indexes the rows (in this case, the column containing the months).

`y=flight_data['NK']` - This sets the column in the data that will be used to determine the height of each bar. In this case, we select the 'NK' column.

**Important Note:** You must select the indexing column with flight_data.index, and it is not possible to use flight_data['Month'] (which will return an error). This is because when we loaded the dataset, the "Month" column was used to index the rows. We always have to use this special notation to select the indexing column.

## Heatmap

We have one more plot type to learn about: heatmaps!

In the code cell below, we create a heatmap to quickly visualize patterns in flight_data. Each cell is color-coded according to its corresponding value.


```python
# Set the width and height of the figure
plt.figure(figsize=(14,6))

# Add title
plt.title("Average Arrival Delay for Each Airline, by Month")

# Heatmap showing average arrival delay for each airline by month
sns.heatmap(data=flight_data, annot=True)

# Add label for horizontal axis
plt.xlabel("Airline")
```




    Text(0.5, 33.0, 'Airline')




    
![png](README_files/README_18_1.png)
    


`annot=True` - This ensures that the values for each cell appear on the chart. (Leaving this out removes the numbers from each of the cells!)

What patterns can you detect in the table? For instance, if you look closely, the months toward the end of the year (especially months 9-11) appear relatively dark for all airlines. This suggests that airlines are better (on average) at keeping schedule during these months!

## Scatter Plot


```python
# Path of the file to read
insurance_filepath = "data/insurance.csv"

# Read the file into a variable insurance_data
insurance_data = pd.read_csv(insurance_filepath)

insurance_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>sex</th>
      <th>bmi</th>
      <th>children</th>
      <th>smoker</th>
      <th>region</th>
      <th>charges</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>19</td>
      <td>female</td>
      <td>27.900</td>
      <td>0</td>
      <td>yes</td>
      <td>southwest</td>
      <td>16884.92400</td>
    </tr>
    <tr>
      <th>1</th>
      <td>18</td>
      <td>male</td>
      <td>33.770</td>
      <td>1</td>
      <td>no</td>
      <td>southeast</td>
      <td>1725.55230</td>
    </tr>
    <tr>
      <th>2</th>
      <td>28</td>
      <td>male</td>
      <td>33.000</td>
      <td>3</td>
      <td>no</td>
      <td>southeast</td>
      <td>4449.46200</td>
    </tr>
    <tr>
      <th>3</th>
      <td>33</td>
      <td>male</td>
      <td>22.705</td>
      <td>0</td>
      <td>no</td>
      <td>northwest</td>
      <td>21984.47061</td>
    </tr>
    <tr>
      <th>4</th>
      <td>32</td>
      <td>male</td>
      <td>28.880</td>
      <td>0</td>
      <td>no</td>
      <td>northwest</td>
      <td>3866.85520</td>
    </tr>
  </tbody>
</table>
</div>



To create a simple scatter plot, we use the `sns.scatterplot` command and specify the values for:

  - the horizontal x-axis (`x=insurance_data['bmi']`)
  - the vertical y-axis (`y=insurance_data['charges']`)


```python
# Set the width and height of the figure
plt.figure(figsize=(14,6))

sns.scatterplot(x=insurance_data['bmi'], y=insurance_data['charges'])
```




    <AxesSubplot:xlabel='bmi', ylabel='charges'>




    
![png](README_files/README_23_1.png)
    


The scatterplot above suggests that body mass index (BMI) and insurance charges are positively correlated, where customers with higher BMI typically also tend to pay more in insurance costs. (This pattern makes sense, since high BMI is typically associated with higher risk of chronic disease.)

To double-check the strength of this relationship, you might like to add a regression line, or the line that best fits the data. We do this by changing the command to `sns.regplot`.


```python
# Set the width and height of the figure
plt.figure(figsize=(14,6))

sns.regplot(x=insurance_data['bmi'], y=insurance_data['charges'])
```




    <AxesSubplot:xlabel='bmi', ylabel='charges'>




    
![png](README_files/README_25_1.png)
    


### Color-coded scatter plots
We can use scatter plots to display the relationships between (not two, but...) three variables! One way of doing this is by color-coding the points.

For instance, to understand how smoking affects the relationship between BMI and insurance costs, we can color-code the points by 'smoker', and plot the other two columns ('bmi', 'charges') on the axes.


```python
# Set the width and height of the figure
plt.figure(figsize=(14,6))

sns.scatterplot(x=insurance_data['bmi'], y=insurance_data['charges'], hue=insurance_data['smoker'])
```




    <AxesSubplot:xlabel='bmi', ylabel='charges'>




    
![png](README_files/README_27_1.png)
    


This scatter plot shows that while nonsmokers to tend to pay slightly more with increasing BMI, smokers pay MUCH more.

To further emphasize this fact, we can use the sns.lmplot command to add two regression lines, corresponding to smokers and nonsmokers. (You'll notice that the regression line for smokers has a much steeper slope, relative to the line for nonsmokers!)


```python
sns.lmplot(x="bmi", y="charges", hue="smoker", data=insurance_data)
```




    <seaborn.axisgrid.FacetGrid at 0x7f1ebda6db50>




    
![png](README_files/README_29_1.png)
    


The `sns.lmplot` command above works slightly differently than the commands you have learned about so far:
`
 - Instead of setting `x=insurance_data['bmi']` to select the `'bmi'` column in insurance_data, we set `x="bmi"` to specify the name of the column only.
 - Similarly, `y="charges"` and `hue="smoker"` also contain the names of columns.
 - We specify the dataset with data=insurance_data.


Finally, there's one more plot that you'll learn about, that might look slightly different from how you're used to seeing scatter plots. Usually, we use scatter plots to highlight the relationship between two continuous variables (like "bmi" and "charges"). However, we can adapt the design of the scatter plot to feature a categorical variable (like "smoker") on one of the main axes. We'll refer to this plot type as a categorical scatter plot, and we build it with the sns.swarmplot command.


```python
# Set the width and height of the figure
plt.figure(figsize=(14,6))

sns.swarmplot(x=insurance_data['smoker'], y=insurance_data['charges'])
```




    <AxesSubplot:xlabel='smoker', ylabel='charges'>




    
![png](README_files/README_31_1.png)
    


## Distributions


```python
# Path of the file to read
iris_filepath = "data/iris.csv"

# Read the file into a variable iris_data
iris_data = pd.read_csv(iris_filepath, index_col="Id")

# Print the first 5 rows of the data
iris_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Sepal Length (cm)</th>
      <th>Sepal Width (cm)</th>
      <th>Petal Length (cm)</th>
      <th>Petal Width (cm)</th>
      <th>Species</th>
    </tr>
    <tr>
      <th>Id</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
  </tbody>
</table>
</div>



### Histograms
Say we would like to create a histogram to see how petal length varies in iris flowers. We can do this with the sns.distplot command.


```python
# Set the width and height of the figure
plt.figure(figsize=(14,6))

sns.distplot(a=iris_data['Petal Length (cm)'], kde=False)
```




    <AxesSubplot:xlabel='Petal Length (cm)'>




    
![png](README_files/README_35_1.png)
    


We customize the behavior of the command with two additional pieces of information:

  - a = chooses the column we'd like to plot (in this case, we chose 'Petal Length (cm)').
  - kde = False is something we'll always provide when creating a histogram, as leaving it out will create a slightly different plot.

### Density plots
The next type of plot is a kernel density estimate (KDE) plot. In case you're not familiar with KDE plots, you can think of it as a smoothed histogram.

To make a KDE plot, we use the sns.kdeplot command. Setting shade=True colors the area below the curve (and data= has identical functionality as when we made the histogram above).


```python
# Set the width and height of the figure
plt.figure(figsize=(14,6))

sns.kdeplot(data=iris_data['Petal Length (cm)'], shade=True)
```




    <AxesSubplot:xlabel='Petal Length (cm)', ylabel='Density'>




    
![png](README_files/README_38_1.png)
    


## 2D KDE plots
We're not restricted to a single column when creating a KDE plot. We can create a two-dimensional (2D) KDE plot with the sns.jointplot command.

In the plot below, the color-coding shows us how likely we are to see different combinations of sepal width and petal length, where darker parts of the figure are more likely.


```python
# Set the width and height of the figure
plt.figure(figsize=(14,6))

sns.jointplot(x=iris_data['Petal Length (cm)'], y=iris_data['Sepal Width (cm)'], kind="kde")
```




    <seaborn.axisgrid.JointGrid at 0x7f1ebd999ca0>




    <Figure size 1008x432 with 0 Axes>



    
![png](README_files/README_40_2.png)
    


Note that in addition to the 2D KDE plot in the center,

  - The curve at the top of the figure is a KDE plot for the data on the x-axis (in this case, `iris_data['Petal Length (cm)']`)
  - The curve on the right of the figure is a KDE plot for the data on the y-axis (in this case, `iris_data['Sepal Width (cm)']`)

### Color-coded plots
For the next part of the tutorial, we'll create plots to understand differences between the species. To accomplish this, we begin by breaking the dataset into three separate files, with one for each species.


```python
# Paths of the files to read
iris_set_filepath = "data/iris_setosa.csv"
iris_ver_filepath = "data/iris_versicolor.csv"
iris_vir_filepath = "data/iris_virginica.csv"

# Read the files into variables 
iris_set_data = pd.read_csv(iris_set_filepath, index_col="Id")
iris_ver_data = pd.read_csv(iris_ver_filepath, index_col="Id")
iris_vir_data = pd.read_csv(iris_vir_filepath, index_col="Id")

# Print the first 5 rows of the Iris versicolor data
iris_ver_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Sepal Length (cm)</th>
      <th>Sepal Width (cm)</th>
      <th>Petal Length (cm)</th>
      <th>Petal Width (cm)</th>
      <th>Species</th>
    </tr>
    <tr>
      <th>Id</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>51</th>
      <td>7.0</td>
      <td>3.2</td>
      <td>4.7</td>
      <td>1.4</td>
      <td>Iris-versicolor</td>
    </tr>
    <tr>
      <th>52</th>
      <td>6.4</td>
      <td>3.2</td>
      <td>4.5</td>
      <td>1.5</td>
      <td>Iris-versicolor</td>
    </tr>
    <tr>
      <th>53</th>
      <td>6.9</td>
      <td>3.1</td>
      <td>4.9</td>
      <td>1.5</td>
      <td>Iris-versicolor</td>
    </tr>
    <tr>
      <th>54</th>
      <td>5.5</td>
      <td>2.3</td>
      <td>4.0</td>
      <td>1.3</td>
      <td>Iris-versicolor</td>
    </tr>
    <tr>
      <th>55</th>
      <td>6.5</td>
      <td>2.8</td>
      <td>4.6</td>
      <td>1.5</td>
      <td>Iris-versicolor</td>
    </tr>
  </tbody>
</table>
</div>



In the code cell below, we create a different histogram for each species by using the sns.distplot command (as above) three times. We use label= to set how each histogram will appear in the legend.


```python
# Set the width and height of the figure
plt.figure(figsize=(14,6))

# Histograms for each species
sns.distplot(a=iris_set_data['Petal Length (cm)'], label="Iris-setosa", kde=False)
sns.distplot(a=iris_ver_data['Petal Length (cm)'], label="Iris-versicolor", kde=False)
sns.distplot(a=iris_vir_data['Petal Length (cm)'], label="Iris-virginica", kde=False)

# Add title
plt.title("Histogram of Petal Lengths, by Species")

# Force legend to appear
plt.legend()
```




    <matplotlib.legend.Legend at 0x7f1ebd5607c0>




    
![png](README_files/README_45_1.png)
    


In this case, the legend does not automatically appear on the plot. To force it to show (for any plot type), we can always use plt.legend().

We can also create a KDE plot for each species by using sns.kdeplot (as above). Again, label= is used to set the values in the legend.


```python
# Set the width and height of the figure
plt.figure(figsize=(14,6))

# KDE plots for each species
sns.kdeplot(data=iris_set_data['Petal Length (cm)'], label="Iris-setosa", shade=True)
sns.kdeplot(data=iris_ver_data['Petal Length (cm)'], label="Iris-versicolor", shade=True)
sns.kdeplot(data=iris_vir_data['Petal Length (cm)'], label="Iris-virginica", shade=True)

# Add title
plt.title("Distribution of Petal Lengths, by Species")
```




    Text(0.5, 1.0, 'Distribution of Petal Lengths, by Species')




    
![png](README_files/README_47_1.png)
    


## Multiple Plots


```python
fig, (ax1, ax2, ax3, ax4) = plt.subplots(1, 4, figsize=(17, 10))
fig.tight_layout(pad=3)  # Set spacing between plots

ax1.set_title("Distribution of Petal Lengths, by Species")
sns.kdeplot(data=iris_set_data['Petal Length (cm)'], label="Iris-setosa", shade=True, ax=ax1)
sns.kdeplot(data=iris_ver_data['Petal Length (cm)'], label="Iris-versicolor", shade=True, ax=ax1)
sns.kdeplot(data=iris_vir_data['Petal Length (cm)'], label="Iris-virginica", shade=True, ax=ax1)

ax2.set_title("Distribution of Petal Lengths, by Species")
sns.kdeplot(data=iris_set_data['Petal Length (cm)'], label="Iris-setosa", shade=True, ax=ax2)
sns.kdeplot(data=iris_ver_data['Petal Length (cm)'], label="Iris-versicolor", shade=True, ax=ax2)
sns.kdeplot(data=iris_vir_data['Petal Length (cm)'], label="Iris-virginica", shade=True, ax=ax2)

ax3.set_title("Distribution of Petal Lengths, by Species")
sns.kdeplot(data=iris_set_data['Petal Length (cm)'], label="Iris-setosa", shade=True, ax=ax3)
sns.kdeplot(data=iris_ver_data['Petal Length (cm)'], label="Iris-versicolor", shade=True, ax=ax3)
sns.kdeplot(data=iris_vir_data['Petal Length (cm)'], label="Iris-virginica", shade=True, ax=ax3)

ax4.set_title("Distribution of Petal Lengths, by Species")
sns.kdeplot(data=iris_set_data['Petal Length (cm)'], label="Iris-setosa", shade=True, ax=ax4)
sns.kdeplot(data=iris_ver_data['Petal Length (cm)'], label="Iris-versicolor", shade=True, ax=ax4)
sns.kdeplot(data=iris_vir_data['Petal Length (cm)'], label="Iris-virginica", shade=True, ax=ax4)
```




    <AxesSubplot:title={'center':'Distribution of Petal Lengths, by Species'}, xlabel='Petal Length (cm)', ylabel='Density'>




    
![png](README_files/README_49_1.png)
    



```python
fig, (ax1, ax2) = plt.subplots(2, 2, figsize=(14, 6))
fig.tight_layout(pad=5.0)  # Set spacing between plots

ax1[0].set_title("Distribution of Petal Lengths, by Species")
sns.kdeplot(data=iris_set_data['Petal Length (cm)'], label="Iris-setosa", shade=True, ax=ax1[0])
sns.kdeplot(data=iris_ver_data['Petal Length (cm)'], label="Iris-versicolor", shade=True, ax=ax1[0])
sns.kdeplot(data=iris_vir_data['Petal Length (cm)'], label="Iris-virginica", shade=True, ax=ax1[0])

ax1[1].set_title("Distribution of Petal Lengths, by Species")
sns.kdeplot(data=iris_set_data['Petal Length (cm)'], label="Iris-setosa", shade=True, ax=ax1[1])
sns.kdeplot(data=iris_ver_data['Petal Length (cm)'], label="Iris-versicolor", shade=True, ax=ax1[1])
sns.kdeplot(data=iris_vir_data['Petal Length (cm)'], label="Iris-virginica", shade=True, ax=ax1[1])

ax2[0].set_title("Distribution of Petal Lengths, by Species")
sns.kdeplot(data=iris_set_data['Petal Length (cm)'], label="Iris-setosa", shade=True, ax=ax2[0])
sns.kdeplot(data=iris_ver_data['Petal Length (cm)'], label="Iris-versicolor", shade=True, ax=ax2[0])
sns.kdeplot(data=iris_vir_data['Petal Length (cm)'], label="Iris-virginica", shade=True, ax=ax2[0])

ax2[1].set_title("Distribution of Petal Lengths, by Species")
sns.kdeplot(data=iris_set_data['Petal Length (cm)'], label="Iris-setosa", shade=True, ax=ax2[1])
sns.kdeplot(data=iris_ver_data['Petal Length (cm)'], label="Iris-versicolor", shade=True, ax=ax2[1])
sns.kdeplot(data=iris_vir_data['Petal Length (cm)'], label="Iris-virginica", shade=True, ax=ax2[1])
```




    <AxesSubplot:title={'center':'Distribution of Petal Lengths, by Species'}, xlabel='Petal Length (cm)', ylabel='Density'>




    
![png](README_files/README_50_1.png)
    

