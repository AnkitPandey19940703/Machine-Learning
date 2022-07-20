```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
```


```python
df = pd.read_csv("https://raw.githubusercontent.com/justmarkham/DAT8/master/data/drinks.csv")
```


```python
df.head()
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
      <th>country</th>
      <th>beer_servings</th>
      <th>spirit_servings</th>
      <th>wine_servings</th>
      <th>total_litres_of_pure_alcohol</th>
      <th>continent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Afghanistan</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>AS</td>
    </tr>
    <tr>
      <td>1</td>
      <td>Albania</td>
      <td>89</td>
      <td>132</td>
      <td>54</td>
      <td>4.9</td>
      <td>EU</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Algeria</td>
      <td>25</td>
      <td>0</td>
      <td>14</td>
      <td>0.7</td>
      <td>AF</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Andorra</td>
      <td>245</td>
      <td>138</td>
      <td>312</td>
      <td>12.4</td>
      <td>EU</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Angola</td>
      <td>217</td>
      <td>57</td>
      <td>45</td>
      <td>5.9</td>
      <td>AF</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 193 entries, 0 to 192
    Data columns (total 6 columns):
    country                         193 non-null object
    beer_servings                   193 non-null int64
    spirit_servings                 193 non-null int64
    wine_servings                   193 non-null int64
    total_litres_of_pure_alcohol    193 non-null float64
    continent                       170 non-null object
    dtypes: float64(1), int64(3), object(2)
    memory usage: 9.2+ KB
    

## Q1: Which continent drinks more beer on average?


```python
df.groupby(by= "continent")["beer_servings"].mean().sort_values(ascending = False)
```




    continent
    EU    193.777778
    SA    175.083333
    OC     89.687500
    AF     61.471698
    AS     37.045455
    Name: beer_servings, dtype: float64



## Q2: For each continent print the statistics for wine consumption.


```python
df.groupby(by = "continent").wine_servings.describe()
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
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
    <tr>
      <th>continent</th>
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
      <td>AF</td>
      <td>53.0</td>
      <td>16.264151</td>
      <td>38.846419</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>13.00</td>
      <td>233.0</td>
    </tr>
    <tr>
      <td>AS</td>
      <td>44.0</td>
      <td>9.068182</td>
      <td>21.667034</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>8.00</td>
      <td>123.0</td>
    </tr>
    <tr>
      <td>EU</td>
      <td>45.0</td>
      <td>142.222222</td>
      <td>97.421738</td>
      <td>0.0</td>
      <td>59.0</td>
      <td>128.0</td>
      <td>195.00</td>
      <td>370.0</td>
    </tr>
    <tr>
      <td>OC</td>
      <td>16.0</td>
      <td>35.625000</td>
      <td>64.555790</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>8.5</td>
      <td>23.25</td>
      <td>212.0</td>
    </tr>
    <tr>
      <td>SA</td>
      <td>12.0</td>
      <td>62.416667</td>
      <td>88.620189</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>12.0</td>
      <td>98.50</td>
      <td>221.0</td>
    </tr>
  </tbody>
</table>
</div>



## Q3: Print the mean alcohol consumption per continent for every column.


```python
df["Total_Alcohol_Consumption"] = df["beer_servings"] + df["spirit_servings"] + df["wine_servings"] +df["total_litres_of_pure_alcohol"]
```


```python
df.head()
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
      <th>country</th>
      <th>beer_servings</th>
      <th>spirit_servings</th>
      <th>wine_servings</th>
      <th>total_litres_of_pure_alcohol</th>
      <th>continent</th>
      <th>Total_Alcohol_Consumption</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Afghanistan</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>AS</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>Albania</td>
      <td>89</td>
      <td>132</td>
      <td>54</td>
      <td>4.9</td>
      <td>EU</td>
      <td>279.9</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Algeria</td>
      <td>25</td>
      <td>0</td>
      <td>14</td>
      <td>0.7</td>
      <td>AF</td>
      <td>39.7</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Andorra</td>
      <td>245</td>
      <td>138</td>
      <td>312</td>
      <td>12.4</td>
      <td>EU</td>
      <td>707.4</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Angola</td>
      <td>217</td>
      <td>57</td>
      <td>45</td>
      <td>5.9</td>
      <td>AF</td>
      <td>324.9</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby(by = "continent").mean()
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
      <th>beer_servings</th>
      <th>spirit_servings</th>
      <th>wine_servings</th>
      <th>total_litres_of_pure_alcohol</th>
      <th>Total_Alcohol_Consumption</th>
    </tr>
    <tr>
      <th>continent</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>AF</td>
      <td>61.471698</td>
      <td>16.339623</td>
      <td>16.264151</td>
      <td>3.007547</td>
      <td>97.083019</td>
    </tr>
    <tr>
      <td>AS</td>
      <td>37.045455</td>
      <td>60.840909</td>
      <td>9.068182</td>
      <td>2.170455</td>
      <td>109.125000</td>
    </tr>
    <tr>
      <td>EU</td>
      <td>193.777778</td>
      <td>132.555556</td>
      <td>142.222222</td>
      <td>8.617778</td>
      <td>477.173333</td>
    </tr>
    <tr>
      <td>OC</td>
      <td>89.687500</td>
      <td>58.437500</td>
      <td>35.625000</td>
      <td>3.381250</td>
      <td>187.131250</td>
    </tr>
    <tr>
      <td>SA</td>
      <td>175.083333</td>
      <td>114.750000</td>
      <td>62.416667</td>
      <td>6.308333</td>
      <td>358.558333</td>
    </tr>
  </tbody>
</table>
</div>



## Q4: Print the median alcohol consumption per continent for every column


```python
df.groupby(by = "continent").median()
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
      <th>beer_servings</th>
      <th>spirit_servings</th>
      <th>wine_servings</th>
      <th>total_litres_of_pure_alcohol</th>
      <th>Total_Alcohol_Consumption</th>
    </tr>
    <tr>
      <th>continent</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>AF</td>
      <td>32.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>2.30</td>
      <td>52.10</td>
    </tr>
    <tr>
      <td>AS</td>
      <td>17.5</td>
      <td>16.0</td>
      <td>1.0</td>
      <td>1.20</td>
      <td>69.20</td>
    </tr>
    <tr>
      <td>EU</td>
      <td>219.0</td>
      <td>122.0</td>
      <td>128.0</td>
      <td>10.00</td>
      <td>550.60</td>
    </tr>
    <tr>
      <td>OC</td>
      <td>52.5</td>
      <td>37.0</td>
      <td>8.5</td>
      <td>1.75</td>
      <td>100.25</td>
    </tr>
    <tr>
      <td>SA</td>
      <td>162.5</td>
      <td>108.5</td>
      <td>12.0</td>
      <td>6.85</td>
      <td>389.85</td>
    </tr>
  </tbody>
</table>
</div>



## Q5: Print the mean, min and max values for spirit consumption.


```python
df.spirit_servings.describe()
```




    count    193.000000
    mean      80.994819
    std       88.284312
    min        0.000000
    25%        4.000000
    50%       56.000000
    75%      128.000000
    max      438.000000
    Name: spirit_servings, dtype: float64




```python
df.groupby(by = "continent").spirit_servings.agg(["mean","min","max"])
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
      <th>mean</th>
      <th>min</th>
      <th>max</th>
    </tr>
    <tr>
      <th>continent</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>AF</td>
      <td>16.339623</td>
      <td>0</td>
      <td>152</td>
    </tr>
    <tr>
      <td>AS</td>
      <td>60.840909</td>
      <td>0</td>
      <td>326</td>
    </tr>
    <tr>
      <td>EU</td>
      <td>132.555556</td>
      <td>0</td>
      <td>373</td>
    </tr>
    <tr>
      <td>OC</td>
      <td>58.437500</td>
      <td>0</td>
      <td>254</td>
    </tr>
    <tr>
      <td>SA</td>
      <td>114.750000</td>
      <td>25</td>
      <td>302</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
