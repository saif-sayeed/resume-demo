---
title: Animated Covid 19 analysis using Python
subtitle: Using Plotly's chloropeth graphs and generic python graphing to visualize Covid 19 infection and death rates and the impact of lockdown in various countries.
# Date published
# date: "2021-07-20T00:00:00Z"
date: "2021-07-20"

# Date updated
# lastmod: "2021-07-20T00:00:00Z"

# readingTime: ten

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Covid 19 Analysis'
  focal_point: ""
  placement: 2
  preview_only: true
---


### Covid 19 analysis using Python

We use Python to animate the spread of covid around the world. Then we focus on a few countries and see how the impact of lockdown has affected the spread of covid in that country. We further see how the infection rates and death rates are correlated.


---


### Importing modules

### Task 1


```python
import pandas as pd
import numpy as np
import plotly.express as px
import matplotlib.pyplot as plt 
print('modules are imported')
```

    modules are imported


### Task 1.1: 
#### Loading the Dataset


```python
dataset_url = 'https://raw.githubusercontent.com/datasets/covid-19/main/data/countries-aggregated.csv'
fname = 'data/countries-aggregated.csv'
df = pd.read_csv(fname)
```


```python
df_31May21 = df[df.Date == '2020-05-31']
```


```python
df_31May21.head()
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
      <th>Date</th>
      <th>Country</th>
      <th>Confirmed</th>
      <th>Recovered</th>
      <th>Deaths</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>130</th>
      <td>2020-05-31</td>
      <td>Afghanistan</td>
      <td>15208</td>
      <td>1328</td>
      <td>258</td>
    </tr>
    <tr>
      <th>658</th>
      <td>2020-05-31</td>
      <td>Albania</td>
      <td>1137</td>
      <td>872</td>
      <td>33</td>
    </tr>
    <tr>
      <th>1186</th>
      <td>2020-05-31</td>
      <td>Algeria</td>
      <td>9394</td>
      <td>5748</td>
      <td>653</td>
    </tr>
    <tr>
      <th>1714</th>
      <td>2020-05-31</td>
      <td>Andorra</td>
      <td>764</td>
      <td>694</td>
      <td>51</td>
    </tr>
    <tr>
      <th>2242</th>
      <td>2020-05-31</td>
      <td>Angola</td>
      <td>86</td>
      <td>18</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>



### Task 1.2:
#### let's check the dataframe 


```python
df_31May21.head()
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
      <th>Date</th>
      <th>Country</th>
      <th>Confirmed</th>
      <th>Recovered</th>
      <th>Deaths</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>130</th>
      <td>2020-05-31</td>
      <td>Afghanistan</td>
      <td>15208</td>
      <td>1328</td>
      <td>258</td>
    </tr>
    <tr>
      <th>658</th>
      <td>2020-05-31</td>
      <td>Albania</td>
      <td>1137</td>
      <td>872</td>
      <td>33</td>
    </tr>
    <tr>
      <th>1186</th>
      <td>2020-05-31</td>
      <td>Algeria</td>
      <td>9394</td>
      <td>5748</td>
      <td>653</td>
    </tr>
    <tr>
      <th>1714</th>
      <td>2020-05-31</td>
      <td>Andorra</td>
      <td>764</td>
      <td>694</td>
      <td>51</td>
    </tr>
    <tr>
      <th>2242</th>
      <td>2020-05-31</td>
      <td>Angola</td>
      <td>86</td>
      <td>18</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_31May21.tail()
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
      <th>Date</th>
      <th>Country</th>
      <th>Confirmed</th>
      <th>Recovered</th>
      <th>Deaths</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>100450</th>
      <td>2020-05-31</td>
      <td>Vietnam</td>
      <td>328</td>
      <td>279</td>
      <td>0</td>
    </tr>
    <tr>
      <th>100978</th>
      <td>2020-05-31</td>
      <td>West Bank and Gaza</td>
      <td>448</td>
      <td>372</td>
      <td>3</td>
    </tr>
    <tr>
      <th>101506</th>
      <td>2020-05-31</td>
      <td>Yemen</td>
      <td>323</td>
      <td>14</td>
      <td>80</td>
    </tr>
    <tr>
      <th>102034</th>
      <td>2020-05-31</td>
      <td>Zambia</td>
      <td>1057</td>
      <td>779</td>
      <td>7</td>
    </tr>
    <tr>
      <th>102562</th>
      <td>2020-05-31</td>
      <td>Zimbabwe</td>
      <td>178</td>
      <td>29</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>



#### let's check the shape of the dataframe 


```python
df_31May21.shape
```




    (195, 5)




```python
df.shape
```




    (102960, 5)



### Task 2.1 :
#### let's do some preprocessing 


```python
dfconf=df[df.Confirmed>0]
```


```python
dfconf.head()
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
      <th>Date</th>
      <th>Country</th>
      <th>Confirmed</th>
      <th>Recovered</th>
      <th>Deaths</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>33</th>
      <td>2020-02-24</td>
      <td>Afghanistan</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>34</th>
      <td>2020-02-25</td>
      <td>Afghanistan</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>35</th>
      <td>2020-02-26</td>
      <td>Afghanistan</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>36</th>
      <td>2020-02-27</td>
      <td>Afghanistan</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>37</th>
      <td>2020-02-28</td>
      <td>Afghanistan</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
dfconf.shape
```




    (91970, 5)



#### let's see data related to a country for example Italy 



```python
dfconf[dfconf.Country=='Italy'].head(10)
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
      <th>Date</th>
      <th>Country</th>
      <th>Confirmed</th>
      <th>Recovered</th>
      <th>Deaths</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>44889</th>
      <td>2020-01-31</td>
      <td>Italy</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>44890</th>
      <td>2020-02-01</td>
      <td>Italy</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>44891</th>
      <td>2020-02-02</td>
      <td>Italy</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>44892</th>
      <td>2020-02-03</td>
      <td>Italy</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>44893</th>
      <td>2020-02-04</td>
      <td>Italy</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>44894</th>
      <td>2020-02-05</td>
      <td>Italy</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>44895</th>
      <td>2020-02-06</td>
      <td>Italy</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>44896</th>
      <td>2020-02-07</td>
      <td>Italy</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>44897</th>
      <td>2020-02-08</td>
      <td>Italy</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>44898</th>
      <td>2020-02-09</td>
      <td>Italy</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



#### let's see Global spread of Covid19

## Code:

```python
fig = px.choropleth(dfconf, locations='Country', locationmode='country names', color='Confirmed', animation_frame='Date')
fig.layout.updatemenus[0].buttons[0].args[1]['frame']['duration'] = 30
fig.layout.updatemenus[0].buttons[0].args[1]['transition']['duration'] = 5
fig.update_geos(projection_type="equirectangular", visible=True, resolution=50)
fig.update_layout(
    title_text = 'Global Spread of Coronavirus',
    title_x = 0.5,
    geo=dict(
        showframe = False,
        showcoastlines = False,
    ))
#fig.show()
iplot(fig,show_link=False)
pio.write_json(fig,"file001.json",engine="json")
fig.write_html("plot001.html")
```

## Chart 1: Global Spread of Covid over Time

![spread of covid](data/covidplot002.gif "Spread of Covid")

Example of Infection rate in China:


# Chart 2:
{{< chart data="ratechina" >}}

 <!-- {{< chart data="file001" >}} -->
 <!-- <iframe
       src="https://github.com/saif-sayeed/resume-demo/blob/master/content/post/covid_analysis_python/ch001.html"
       width="90%"
       height="500px"
       style="border:none;">
 </iframe> -->---
#### let's see Global spread of Covid19
title: Chk Part 02
---


### Let's see Global deaths of Covid19


```python
dfdeaths=df[df.Deaths>0]
```


```python
dfdeaths.head()
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
      <th>Date</th>
      <th>Country</th>
      <th>Confirmed</th>
      <th>Recovered</th>
      <th>Deaths</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>60</th>
      <td>2020-03-22</td>
      <td>Afghanistan</td>
      <td>34</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>61</th>
      <td>2020-03-23</td>
      <td>Afghanistan</td>
      <td>41</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>62</th>
      <td>2020-03-24</td>
      <td>Afghanistan</td>
      <td>43</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>63</th>
      <td>2020-03-25</td>
      <td>Afghanistan</td>
      <td>76</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>64</th>
      <td>2020-03-26</td>
      <td>Afghanistan</td>
      <td>80</td>
      <td>2</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
dfdeaths.shape
```




    (81987, 5)


## Chart 2: Global Deaths from Covid

![Global Deaths from Covid](data/gdc4xlowres3.gif "Global Deaths from Covid")
