```python
# import dependencies
import pandas as pd

# grabbing the csv file to be loaded
load_file = "Resources/purchase_data.csv"

# reading the csv and storing into a data frame
purchase_data = pd.read_csv(load_file)
```


```python
# find number of players from the list of screen names
players_list = purchase_data["SN"].unique()
player_count = len(players_list)

# store the count in a basic data frame and display
total_players = pd.DataFrame([{"Total Players": player_count}])
total_players
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
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>576</td>
    </tr>
  </tbody>
</table>
</div>




```python
# calculate summary data
unique_items = purchase_data["Item Name"].nunique()
average_price = purchase_data["Price"].mean()
number_purchases = purchase_data["Purchase ID"].count()
total_revenue = purchase_data["Price"].sum()

# store the summary data in a data frame
purchase_summary = [{"Number of Unique Items": unique_items,
                     "Average Price": average_price,
                     "Number of Purchases": number_purchases,
                     "Total Revenue": total_revenue}]
purchase_summary_df = pd.DataFrame(purchase_summary)

# format the data to represent monetary values
purchase_summary_df["Average Price"] = purchase_summary_df["Average Price"].map("${:.2f}".format)
purchase_summary_df["Total Revenue"] = purchase_summary_df["Total Revenue"].map("${:.2f}".format)

# display the summary data frame
purchase_summary_df
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
      <th>Number of Unique Items</th>
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>179</td>
      <td>$3.05</td>
      <td>780</td>
      <td>$2379.77</td>
    </tr>
  </tbody>
</table>
</div>




```python
# group the data frame by gender
gender_group = purchase_data.groupby(["Gender"])

# determine count and percentages of gender
gender_counts = gender_group["SN"].nunique()
gender_percents = gender_counts / player_count * 100

# store the count and percentage in a data frame
gender_demo_df = pd.DataFrame({"Total Count": gender_counts, 
                               "Percentage of Players": gender_percents}) 

# format the percentage column and sort the data frame
gender_demo_df["Percentage of Players"] = gender_demo_df["Percentage of Players"].map("{:.2f}%".format)
sorted_gender_demo_df = gender_demo_df.sort_values(["Total Count"], ascending=False)

# display the data frame
sorted_gender_demo_df
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
      <th>Total Count</th>
      <th>Percentage of Players</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>484</td>
      <td>84.03%</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>81</td>
      <td>14.06%</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
      <td>1.91%</td>
    </tr>
  </tbody>
</table>
</div>




```python
# calculate purchase data
gender_purchase_count = gender_group["Purchase ID"].count()
gender_average_purchase_price = gender_group["Price"].mean()
gender_total_purchase_value = gender_group["Price"].sum()
gender_average_total_purchase_per = gender_total_purchase_value / gender_counts

# store the data in a data frame
gender_purchases = {"Purchase Count": gender_purchase_count,
                    "Average Purchase Price": gender_average_purchase_price,
                    "Total Purchase Value": gender_total_purchase_value,
                    "Avg Total Purchase per Person": gender_average_total_purchase_per}
gender_purchases_df = pd.DataFrame(gender_purchases)

# format the data to represent monetary values
gender_purchases_df["Average Purchase Price"] = gender_purchases_df["Average Purchase Price"].map("${:.2f}".format)
gender_purchases_df["Total Purchase Value"] = gender_purchases_df["Total Purchase Value"].map("${:.2f}".format)
gender_purchases_df["Avg Total Purchase per Person"] = gender_purchases_df["Avg Total Purchase per Person"].map("${:.2f}".format)

# display the data frame
gender_purchases_df
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Avg Total Purchase per Person</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>113</td>
      <td>$3.20</td>
      <td>$361.94</td>
      <td>$4.47</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>652</td>
      <td>$3.02</td>
      <td>$1967.64</td>
      <td>$4.07</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>15</td>
      <td>$3.35</td>
      <td>$50.19</td>
      <td>$4.56</td>
    </tr>
  </tbody>
</table>
</div>




```python
# establish bins for age groups
age_bins = [0, 9.9, 14.9, 19.9, 24.9, 29.9, 34.9, 39.9, 100]
age_labels = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"]

# categorize age group data using bins
purchase_data["Age Group"] = pd.cut(purchase_data["Age"], age_bins, labels=age_labels)

# calculate age data
age_groups = purchase_data.groupby(["Age Group"])
age_counts = age_groups["SN"].nunique()
age_percents = age_counts / player_count * 100

# store the data in a data frame
age_demo_df = pd.DataFrame({"Total Count": age_counts, "Percentage of Players": age_percents})

# format the data to represent percenatages
age_demo_df["Percentage of Players"] = age_demo_df["Percentage of Players"].map("{:.2f}%".format)

# display the data frame
age_demo_df
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
      <th>Total Count</th>
      <th>Percentage of Players</th>
    </tr>
    <tr>
      <th>Age Group</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>17</td>
      <td>2.95%</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>22</td>
      <td>3.82%</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>107</td>
      <td>18.58%</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>258</td>
      <td>44.79%</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>77</td>
      <td>13.37%</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>52</td>
      <td>9.03%</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>31</td>
      <td>5.38%</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>12</td>
      <td>2.08%</td>
    </tr>
  </tbody>
</table>
</div>




```python
# calculate purchase data
age_purchase_count = age_groups["Purchase ID"].count()
age_average_purchase_price = age_groups["Price"].mean()
age_total_purchase_value = age_groups["Price"].sum()
age_average_total_purchase_per = age_total_purchase_value / age_counts

# store the data in a data frame
age_purchases = {"Purchase Count": age_purchase_count,
                    "Average Purchase Price": age_average_purchase_price,
                    "Total Purchase Value": age_total_purchase_value,
                    "Avg Total Purchase per Person": age_average_total_purchase_per}
age_purchases_df = pd.DataFrame(age_purchases)

# format the data to represent monetary values
age_purchases_df["Average Purchase Price"] = age_purchases_df["Average Purchase Price"].map("${:.2f}".format)
age_purchases_df["Total Purchase Value"] = age_purchases_df["Total Purchase Value"].map("${:.2f}".format)
age_purchases_df["Avg Total Purchase per Person"] = age_purchases_df["Avg Total Purchase per Person"].map("${:.2f}".format)

# display the data frame
age_purchases_df
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Avg Total Purchase per Person</th>
    </tr>
    <tr>
      <th>Age Group</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>23</td>
      <td>$3.35</td>
      <td>$77.13</td>
      <td>$4.54</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>28</td>
      <td>$2.96</td>
      <td>$82.78</td>
      <td>$3.76</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>136</td>
      <td>$3.04</td>
      <td>$412.89</td>
      <td>$3.86</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>365</td>
      <td>$3.05</td>
      <td>$1114.06</td>
      <td>$4.32</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>101</td>
      <td>$2.90</td>
      <td>$293.00</td>
      <td>$3.81</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>73</td>
      <td>$2.93</td>
      <td>$214.00</td>
      <td>$4.12</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>41</td>
      <td>$3.60</td>
      <td>$147.67</td>
      <td>$4.76</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>13</td>
      <td>$2.94</td>
      <td>$38.24</td>
      <td>$3.19</td>
    </tr>
  </tbody>
</table>
</div>




```python
# group the dataframe by individual screen names (users/spenders)
spender_group = purchase_data.groupby(["SN"])

# calculate the data for each spender
spend_counts = spender_group["Purchase ID"].count()
spend_average = spender_group["Price"].mean()
spend_totals = spender_group["Price"].sum()

# store the data in a dataframe
spender_purchases = {"Purchase Count": spend_counts,
                    "Average Purchase Price": spend_average,
                    "Total Purchase Value": spend_totals}
spender_purchases_df = pd.DataFrame(spender_purchases)

# sort the data frame by the total spent
spender_purchases_df = spender_purchases_df.sort_values(["Total Purchase Value"], ascending=False)

# format the data to represent monetary values
spender_purchases_df["Average Purchase Price"] = spender_purchases_df["Average Purchase Price"].map("${:.2f}".format)
spender_purchases_df["Total Purchase Value"] = spender_purchases_df["Total Purchase Value"].map("${:.2f}".format)

# display a data frame of the top 5 spenders
top_five_spenders_df = spender_purchases_df.head(5)
top_five_spenders_df
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
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
      <th>Lisosia93</th>
      <td>5</td>
      <td>$3.79</td>
      <td>$18.96</td>
    </tr>
    <tr>
      <th>Idastidru52</th>
      <td>4</td>
      <td>$3.86</td>
      <td>$15.45</td>
    </tr>
    <tr>
      <th>Chamjask73</th>
      <td>3</td>
      <td>$4.61</td>
      <td>$13.83</td>
    </tr>
    <tr>
      <th>Iral74</th>
      <td>4</td>
      <td>$3.40</td>
      <td>$13.62</td>
    </tr>
    <tr>
      <th>Iskadarya95</th>
      <td>3</td>
      <td>$4.37</td>
      <td>$13.10</td>
    </tr>
  </tbody>
</table>
</div>




```python
# pull the Item ID, Item Name, and Price columns and group the data by ID and Name
popular_items_df = purchase_data[["Item ID", "Item Name", "Price"]]
group_popular_items = popular_items_df.groupby(["Item ID", "Item Name"])

# calculate the data for each unique item
popular_counts = group_popular_items["Item ID"].count()
popular_total_purchase_value = group_popular_items["Price"].sum()
popular_price = popular_total_purchase_value / popular_counts

# store the data in a dataframe
popular_purchases = {"Purchase Count": popular_counts,
                    "Item Price": popular_price,
                    "Total Purchase Value": popular_total_purchase_value}
popular_purchases_df = pd.DataFrame(popular_purchases)

# sort the data frame by purchase count
countsort_popular_purchases_df = popular_purchases_df.sort_values("Purchase Count", ascending=False)

# format the data to represent monetary values
countsort_popular_purchases_df["Item Price"] = countsort_popular_purchases_df["Item Price"].map("${:.2f}".format)
countsort_popular_purchases_df["Total Purchase Value"] = countsort_popular_purchases_df["Total Purchase Value"].map("${:.2f}".format)

# display a data frame of the top five most popular items (by purchase count)
five_most_popular_items_df = countsort_popular_purchases_df.head(5)
five_most_popular_items_df
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
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>92</th>
      <th>Final Critic</th>
      <td>13</td>
      <td>$4.61</td>
      <td>$59.99</td>
    </tr>
    <tr>
      <th>178</th>
      <th>Oathbreaker, Last Hope of the Breaking Storm</th>
      <td>12</td>
      <td>$4.23</td>
      <td>$50.76</td>
    </tr>
    <tr>
      <th>145</th>
      <th>Fiery Glass Crusader</th>
      <td>9</td>
      <td>$4.58</td>
      <td>$41.22</td>
    </tr>
    <tr>
      <th>132</th>
      <th>Persuasion</th>
      <td>9</td>
      <td>$3.22</td>
      <td>$28.99</td>
    </tr>
    <tr>
      <th>108</th>
      <th>Extraction, Quickblade Of Trembling Hands</th>
      <td>9</td>
      <td>$3.53</td>
      <td>$31.77</td>
    </tr>
  </tbody>
</table>
</div>




```python
# sort the data frame of purchase data for unique items, by the total purchased value
totalsort_popular_purchases_df = popular_purchases_df.sort_values("Total Purchase Value", ascending=False)

# format the data to represent monetary values
totalsort_popular_purchases_df["Item Price"] = totalsort_popular_purchases_df["Item Price"].map("${:.2f}".format)
totalsort_popular_purchases_df["Total Purchase Value"] = totalsort_popular_purchases_df["Total Purchase Value"].map("${:.2f}".format)

# display a data frame of the top five most popular items (by total purchased value)
five_most_profitable_items_df = totalsort_popular_purchases_df.head(5)
five_most_profitable_items_df
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
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>92</th>
      <th>Final Critic</th>
      <td>13</td>
      <td>$4.61</td>
      <td>$59.99</td>
    </tr>
    <tr>
      <th>178</th>
      <th>Oathbreaker, Last Hope of the Breaking Storm</th>
      <td>12</td>
      <td>$4.23</td>
      <td>$50.76</td>
    </tr>
    <tr>
      <th>82</th>
      <th>Nirvana</th>
      <td>9</td>
      <td>$4.90</td>
      <td>$44.10</td>
    </tr>
    <tr>
      <th>145</th>
      <th>Fiery Glass Crusader</th>
      <td>9</td>
      <td>$4.58</td>
      <td>$41.22</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Singed Scalpel</th>
      <td>8</td>
      <td>$4.35</td>
      <td>$34.80</td>
    </tr>
  </tbody>
</table>
</div>


