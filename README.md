# PandasHW


```python
# Dependencies
import os
import pandas as pd
import numpy as pn
```


```python
# Read in JSON file
purchase_data = pd.read_json("../HeroesofPymoli/purchase_data.json")
purchase_data.head(10)
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
    <tr>
      <th>5</th>
      <td>20</td>
      <td>Male</td>
      <td>10</td>
      <td>Sleepwalker</td>
      <td>1.73</td>
      <td>Tanimnya91</td>
    </tr>
    <tr>
      <th>6</th>
      <td>20</td>
      <td>Male</td>
      <td>153</td>
      <td>Mercenary Sabre</td>
      <td>4.57</td>
      <td>Undjaskla97</td>
    </tr>
    <tr>
      <th>7</th>
      <td>29</td>
      <td>Female</td>
      <td>169</td>
      <td>Interrogator, Blood Blade of the Queen</td>
      <td>3.32</td>
      <td>Iathenudil29</td>
    </tr>
    <tr>
      <th>8</th>
      <td>25</td>
      <td>Male</td>
      <td>118</td>
      <td>Ghost Reaver, Longsword of Magic</td>
      <td>2.77</td>
      <td>Sondenasta63</td>
    </tr>
    <tr>
      <th>9</th>
      <td>31</td>
      <td>Male</td>
      <td>99</td>
      <td>Expiration, Warscythe Of Lost Worlds</td>
      <td>4.53</td>
      <td>Hilaerin92</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Find the Total Number of Players
total_players = len(purchase_data["Item ID"].unique())

# Place the data into a summary DataFrame
summary_table = pd.DataFrame({"Total Number of Players": [total_players]})
summary_table
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
      <th>Total Number of Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>183</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Total the number of unique Items
item_count = len(purchase_data["Item Name"].unique())
print(item_count)

# Find the average purchase price
avg_price = purchase_data["Price"].mean()
print(avg_price)

# Total the number of purchases
purchase_count = len((purchase_data["Price"]))
print(purchase_count)

# Find the Total Revenue using the "sum" function on the Price column
total_revenue = purchase_data["Price"].sum()
print(total_revenue)
```

    179
    2.931192307692303
    780
    2286.33



```python
# Place all of the data found into a summary DataFrame
summary_table = pd.DataFrame({"Number of Unique Items": [item_count],
                              "Average Purchase Price": [avg_price],
                              "Total Purchases": [purchase_count], 
                              "Total Revenue": [total_revenue]})
summary_table

# Use Map to format the appropriate columns
summary_table["Average Purchase Price"] = summary_table["Average Purchase Price"].map("${:.2f}".format)
summary_table["Total Revenue"] = summary_table["Total Revenue"].map("${:.2f}".format)
summary_table
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
      <th>Average Purchase Price</th>
      <th>Number of Unique Items</th>
      <th>Total Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>$2.93</td>
      <td>179</td>
      <td>780</td>
      <td>$2286.33</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Group by Gender
gender_groups = purchase_data["Gender"].unique()
print(gender_groups)

gender_counts = purchase_data["Gender"].value_counts()
print(gender_counts)

gender_table = pd.DataFrame(gender_counts)
gender_table
```

    ['Male' 'Female' 'Other / Non-Disclosed']
    Male                     633
    Female                   136
    Other / Non-Disclosed     11
    Name: Gender, dtype: int64





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
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>633</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>136</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
percent_genders = (gender_table.Gender/gender_table.Gender.sum()).mul(100).round(2).astype(str)+'%'
print(percent_genders)

gender_summary = pd.DataFrame({"Gender": ["Male", "Female", "Other/Non-Disclosed"], 
                              "Percentage of Players": [81.15, 17.44, 1.41], 
                              "Total Count": [633, 136, 11]})
gender_summary.set_index("Gender")
gender_summary["Percentage of Players"] = gender_summary["Percentage of Players"].map("{:.2f}%".format)

gender_totals = gender_summary.groupby("Gender")
gender_totals.max()
```

    Male                     81.15%
    Female                   17.44%
    Other / Non-Disclosed     1.41%
    Name: Gender, dtype: object





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
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>17.44%</td>
      <td>136</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>81.15%</td>
      <td>633</td>
    </tr>
    <tr>
      <th>Other/Non-Disclosed</th>
      <td>1.41%</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create a new DataFrame that looks into a specific genders
male_data = purchase_data.loc[purchase_data["Gender"] == "Male"]
male_df = pd.DataFrame(male_data)
male_df.head()

# Find the average purchase price
male_avg_price = male_df["Price"].mean()
print(male_avg_price)

# Total the number of purchases
male_purchase_count = len((male_df["Price"]))
print(male_purchase_count)

# Find the Total Revenue using the "sum" function on the Price column
male_total_revenue = male_df["Price"].sum()
print(male_total_revenue)
```

    2.9505213270142154
    633
    1867.68



```python
female_data = purchase_data.loc[purchase_data["Gender"] == "Female"]
female_df = pd.DataFrame(female_data)
female_df.head()

# Find the average purchase price
female_avg_price = female_df["Price"].mean()
print(female_avg_price)

# Total the number of purchases
female_purchase_count = len((female_df["Price"]))
print(female_purchase_count)

# Find the Total Revenue using the "sum" function on the Price column
female_total_revenue = female_df["Price"].sum()
print(female_total_revenue)
```

    2.815514705882352
    136
    382.90999999999997



```python
other_data = purchase_data.loc[purchase_data["Gender"] == "Other / Non-Disclosed"]
other_df = pd.DataFrame(other_data)
other_df.head()

# Find the average purchase price
other_avg_price = other_df["Price"].mean()
print(other_avg_price)

# Total the number of purchases
other_purchase_count = len((other_df["Price"]))
print(other_purchase_count)

# Find the Total Revenue using the "sum" function on the Price column
other_total_revenue = other_df["Price"].sum()
print(other_total_revenue)
```

    3.2490909090909086
    11
    35.739999999999995



```python
# Create a DataFrame depicting the calculated numbers for a purchasing analysis by gender
gender_df = pd.DataFrame({"Gender": ["Male", "Female", "Other/Non-Disclosed"], 
                                           "Purchase Count": [633, 136, 11], 
                                           "Average Purchase Price": [2.95, 2.82, 3.25], 
                                           "Total Purchase Value": [1867.68, 382.91, 35.74]})
gender_df.set_index("Gender")
gender_df["Average Purchase Price"] = gender_df["Average Purchase Price"].map("${:.2f}".format)
gender_df["Total Purchase Value"] = gender_df["Total Purchase Value"].map("${:.2f}".format)
gender_df 

purchasing_analysis_gender = gender_df.groupby("Gender")
purchasing_analysis_gender.max()
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
      <th>Average Purchase Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>$2.82</td>
      <td>136</td>
      <td>$382.91</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>$2.95</td>
      <td>633</td>
      <td>$1867.68</td>
    </tr>
    <tr>
      <th>Other/Non-Disclosed</th>
      <td>$3.25</td>
      <td>11</td>
      <td>$35.74</td>
    </tr>
  </tbody>
</table>
</div>




```python
print(purchase_data["Age"].max())
```

    45



```python
age_counts = purchase_data["Age"].value_counts()
age_counts.head()
```




    20    98
    24    70
    22    68
    25    67
    23    57
    Name: Age, dtype: int64




```python
# Create bins in which to place values based upon TED Talk views
bins = [0, 10, 14, 19, 24, 29, 34, 39, 40]

# Create labels for these bins
group_labels = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"]

# Slice the data and place it into bins
pd.cut(purchase_data["Age"], bins, labels=group_labels)

# Place the data series into a new column inside of the Purchase Data
purchase_data["Age_Group"] = pd.cut(purchase_data["Age"], bins, labels=group_labels)
purchase_data.head()
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>Age Group</th>
      <th>Age_Group</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
      <td>35-39</td>
      <td>35-39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
      <td>20-24</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
      <td>30-34</td>
      <td>30-34</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
      <td>20-24</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
      <td>20-24</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create a GroupBy object based upon "Age Group"
age_group = purchase_data.groupby("Age_Group")
age_group.max()

# Find how many rows fall into each bin
age_group_totals = pd.DataFrame(age_group["Age_Group"].count())
age_group_totals

percent_age = (age_group_totals.Age_Group/age_group_totals.Age_Group.sum()).mul(100).round(2).astype(str)+'%'

age_group_totals["Percentage of Players"] = percent_age
age_group_totals
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
      <th>Age_Group</th>
      <th>Percentage of Players</th>
    </tr>
    <tr>
      <th>Age_Group</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>32</td>
      <td>4.12%</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>31</td>
      <td>3.99%</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>133</td>
      <td>17.12%</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>336</td>
      <td>43.24%</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>125</td>
      <td>16.09%</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>64</td>
      <td>8.24%</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>42</td>
      <td>5.41%</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>14</td>
      <td>1.8%</td>
    </tr>
  </tbody>
</table>
</div>




```python
### Organize <10 age group data
lt_10 = purchase_data.loc[purchase_data["Age_Group"] == "<10"]
lt_10_df = pd.DataFrame(lt_10)
lt_10_df.head()

# Find the average purchase price
lt10_avg_price = lt_10_df["Price"].mean()
print(lt10_avg_price)

# Total the number of purchases
lt10_purchase_count = len((lt_10_df["Price"]))
print(lt10_purchase_count)

# Find the Total Revenue using the "sum" function on the Price column
lt10_total_revenue = lt_10_df["Price"].sum()
print(lt10_total_revenue)

#_____________________________________________________________________
### Organize 10-14 age group data
bw_10_14 = purchase_data.loc[purchase_data["Age_Group"] == "10-14"]
bw_10_14_df = pd.DataFrame(bw_10_14)
bw_10_14_df.head()

# Find the average purchase price
bw_10_14_avg_price = bw_10_14_df["Price"].mean()
print(bw_10_14_avg_price)

# Total the number of purchases
bw_10_14_purchase_count = len((bw_10_14_df["Price"]))
print(bw_10_14_purchase_count)

# Find the Total Revenue using the "sum" function on the Price column
bw_10_14_total_revenue = bw_10_14_df["Price"].sum()
print(bw_10_14_total_revenue)

#_____________________________________________________________________
### Organize 15-19 age group data
bw_15_19 = purchase_data.loc[purchase_data["Age_Group"] == "15-19"]
bw_15_19_df = pd.DataFrame(bw_15_19)
bw_15_19_df.head()

# Find the average purchase price
bw_15_19_avg_price = bw_15_19_df["Price"].mean()
print(bw_15_19_avg_price)

# Total the number of purchases
bw_15_19_purchase_count = len((bw_15_19_df["Price"]))
print(bw_15_19_purchase_count)

# Find the Total Revenue using the "sum" function on the Price column
bw_15_19_total_revenue = bw_15_19_df["Price"].sum()
print(bw_15_19_total_revenue)

#_____________________________________________________________________
### Organize 20-24 age group data
bw_20_24 = purchase_data.loc[purchase_data["Age_Group"] == "20-24"]
bw_20_24_df = pd.DataFrame(bw_20_24)
bw_20_24_df.head()

# Find the average purchase price
bw_20_24_avg_price = bw_20_24_df["Price"].mean()
print(bw_20_24_avg_price)

# Total the number of purchases
bw_20_24_purchase_count = len((bw_20_24_df["Price"]))
print(bw_20_24_purchase_count)

# Find the Total Revenue using the "sum" function on the Price column
bw_20_24_total_revenue = bw_20_24_df["Price"].sum()
print(bw_20_24_total_revenue)

#_____________________________________________________________________
### Organize 25-29 age group data
bw_25_29 = purchase_data.loc[purchase_data["Age_Group"] == "25-29"]
bw_25_29_df = pd.DataFrame(bw_25_29)
bw_25_29_df.head()

# Find the average purchase price
bw_25_29_avg_price = bw_25_29_df["Price"].mean()
print(bw_25_29_avg_price)

# Total the number of purchases
bw_25_29_purchase_count = len((bw_25_29_df["Price"]))
print(bw_25_29_purchase_count)

# Find the Total Revenue using the "sum" function on the Price column
bw_25_29_total_revenue = bw_25_29_df["Price"].sum()
print(bw_25_29_total_revenue)

#_____________________________________________________________________
### Organize 30-34 age group data
bw_30_34 = purchase_data.loc[purchase_data["Age_Group"] == "30-34"]
bw_30_34_df = pd.DataFrame(bw_30_34)
bw_30_34_df.head()

# Find the average purchase price
bw_30_34_avg_price = bw_30_34_df["Price"].mean()
print(bw_30_34_avg_price)

# Total the number of purchases
bw_30_34_purchase_count = len((bw_30_34_df["Price"]))
print(bw_30_34_purchase_count)

# Find the Total Revenue using the "sum" function on the Price column
bw_30_34_total_revenue = bw_30_34_df["Price"].sum()
print(bw_30_34_total_revenue)

#_____________________________________________________________________
### Organize 35-39 age group data
bw_35_39 = purchase_data.loc[purchase_data["Age_Group"] == "35-39"]
bw_35_39_df = pd.DataFrame(bw_35_39)
bw_35_39_df.head()

# Find the average purchase price
bw_35_39_avg_price = bw_35_39_df["Price"].mean()
print(bw_35_39_avg_price)

# Total the number of purchases
bw_35_39_purchase_count = len((bw_35_39_df["Price"]))
print(bw_35_39_purchase_count)

# Find the Total Revenue using the "sum" function on the Price column
bw_35_39_total_revenue = bw_35_39_df["Price"].sum()
print(bw_35_39_total_revenue)

#_____________________________________________________________________
### Organize 40+ age group data
gt_40 = purchase_data.loc[purchase_data["Age_Group"] == "40+"]
gt_40_df = pd.DataFrame(gt_40)
gt_40_df.head()

# Find the average purchase price
gt_40_avg_price = gt_40_df["Price"].mean()
print(gt_40_avg_price)

# Total the number of purchases
gt_40_purchase_count = len((gt_40_df["Price"]))
print(gt_40_purchase_count)

# Find the Total Revenue using the "sum" function on the Price column
gt_40_total_revenue = gt_40_df["Price"].sum()
print(gt_40_total_revenue)
```

    3.0193749999999993
    32
    96.62
    2.7029032258064514
    31
    83.78999999999999
    2.905413533834586
    133
    386.41999999999996
    2.913005952380953
    336
    978.77
    2.96264
    125
    370.33
    3.082031249999999
    64
    197.25
    2.842857142857143
    42
    119.4
    3.222142857142857
    14
    45.11



```python
# Create a DataFrame depicting the calculated numbers for a purchasing analysis by age
age_df = pd.DataFrame({"Age Group": ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"], 
                                           "Purchase Count": [32, 31, 133, 336, 125, 64, 42, 14], 
                                           "Average Purchase Price": [3.02, 2.70, 2.91, 2.91, 2.96, 3.08, 2.84, 3.22], 
                                           "Total Purchase Value": [96.62, 83.79, 386.42, 978.77, 370.33, 197.25, 119.40, 45.11]})
age_df.set_index("Age Group")
age_df["Average Purchase Price"] = age_df["Average Purchase Price"].map("${:.2f}".format)
age_df["Total Purchase Value"] = age_df["Total Purchase Value"].map("${:.2f}".format)
age_df

purchasing_analysis_age = age_df.groupby("Age Group")
purchasing_analysis_age.max()
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
      <th>Average Purchase Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Age Group</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10-14</th>
      <td>$2.70</td>
      <td>31</td>
      <td>$83.79</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>$2.91</td>
      <td>133</td>
      <td>$386.42</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>$2.91</td>
      <td>336</td>
      <td>$978.77</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>$2.96</td>
      <td>125</td>
      <td>$370.33</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>$3.08</td>
      <td>64</td>
      <td>$197.25</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>$2.84</td>
      <td>42</td>
      <td>$119.40</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>$3.22</td>
      <td>14</td>
      <td>$45.11</td>
    </tr>
    <tr>
      <th>&lt;10</th>
      <td>$3.02</td>
      <td>32</td>
      <td>$96.62</td>
    </tr>
  </tbody>
</table>
</div>




```python
SN_groups = purchase_data.groupby(["SN"]).sum().sort_values("Price", ascending=False)
SN_groups.head()
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
      <th>Age</th>
      <th>Item ID</th>
      <th>Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Undirrala66</th>
      <td>145</td>
      <td>472</td>
      <td>17.06</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>100</td>
      <td>233</td>
      <td>13.56</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>156</td>
      <td>609</td>
      <td>12.74</td>
    </tr>
    <tr>
      <th>Haellysu29</th>
      <td>63</td>
      <td>353</td>
      <td>12.73</td>
    </tr>
    <tr>
      <th>Eoda93</th>
      <td>66</td>
      <td>284</td>
      <td>11.58</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create a GroupBy object based upon "Item Name"
Item_groups = purchase_data.groupby(["Item Name"]).sum().sort_values("Price", ascending=False)
Item_groups.head()
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
      <th>Age</th>
      <th>Item ID</th>
      <th>Price</th>
    </tr>
    <tr>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Final Critic</th>
      <td>350</td>
      <td>1342</td>
      <td>38.60</td>
    </tr>
    <tr>
      <th>Retribution Axe</th>
      <td>234</td>
      <td>306</td>
      <td>37.26</td>
    </tr>
    <tr>
      <th>Stormcaller</th>
      <td>241</td>
      <td>1050</td>
      <td>34.65</td>
    </tr>
    <tr>
      <th>Spectral Diamond Doomblade</th>
      <td>154</td>
      <td>805</td>
      <td>29.75</td>
    </tr>
    <tr>
      <th>Orenmir</th>
      <td>140</td>
      <td>192</td>
      <td>29.70</td>
    </tr>
  </tbody>
</table>
</div>



3 Observable Trends

1)  The biggest noticeable trend is that the age group of 20-24 year olds is by far the top spending group by age, spending almost thre times as much as the next highest spenders (15-19 year olds).

2)  There are roughly four times as many male gamers versus female gamers.  This translates to males making 6 times as many purchases and spending almost 6 times as much on the game as female gamers do.

3)  The user that spent the most was 'Undirrala66' and the top two most purchased items were the 'Final Critic' and the 'Retribution Axe'.
