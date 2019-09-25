
### Note
* Instructions have been included for each segment. You do not have to follow them exactly, but they are included to help you think through the steps.


```python
# Dependencies and Setup
import pandas as pd

# File to Load (Remember to Change These)
file_to_load = "Resources/purchase_data.csv"

# Read Purchasing File and store into Pandas data frame
purchase_data = pd.read_csv(file_to_load)
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
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
    </tr>
    <tr>
      <td>1</td>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
    </tr>
    <tr>
      <td>2</td>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
    </tr>
    <tr>
      <td>3</td>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
    </tr>
    <tr>
      <td>4</td>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
    </tr>
  </tbody>
</table>
</div>



## Player Count

* Display the total number of players



```python
#Count the length of the column SN which are the number of unique players purchasing items
total_players = len(purchase_data["SN"].value_counts())

# Create a data frame with total players named player summary
player_sum_df = pd.DataFrame( {"Player Summary": [total_players] } )
player_sum_df
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
      <th>Player Summary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>576</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Total)

* Run basic calculations to obtain number of unique items, average price, etc.


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame



```python
#number of Unique Items by Item ID
unique_item = len(purchase_data["Item ID"].unique())

#average of the price columns
avg_price = (purchase_data["Price"]).mean()

#total number of purchases
total_purchases = (purchase_data["Purchase ID"]).count()

#total revenue of price column
total_revenue = (purchase_data ["Price"]).sum()

#display the summary of information
summary_df = pd.DataFrame({"Number of Unique Items": [unique_item], 
                           "Average Price":[avg_price], 
                            "Number of Purchases" : [total_purchases],
                              "Total Revenue": [total_revenue]})

summary_df

#OPTIONAL give the displayed data cleaner formatting.
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
      <td>0</td>
      <td>183</td>
      <td>3.050987</td>
      <td>780</td>
      <td>2379.77</td>
    </tr>
  </tbody>
</table>
</div>



## Gender Demographics

* Percentage and Count of Male Players


* Percentage and Count of Female Players


* Percentage and Count of Other / Non-Disclosed





```python
#dataframe of gender
gender_group = purchase_data.groupby(["Gender"]).nunique()
#gender_group = purchase_data.groupby ("Gender")

#total number of items in gender dataframe
total_gender = gender_group["SN"]
#total_gender

#percentage of players = map("{:,.2%}".format)
total_percent = total_gender / total_players
#total_percent

summary_percentage_df = {"Total Count" : total_gender, 
                          "Percentage of Players" : total_percent}

summary_percent_df = pd.DataFrame(summary_percentage_df)


#Formatting

summary_percent_df["Percentage of Players"] = summary_percent_df["Percentage of Players"].map("{:,.2f}".format)

summary_percent_df.sort_values(["Total Count"], ascending=False)
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
      <td>Male</td>
      <td>484</td>
      <td>0.84</td>
    </tr>
    <tr>
      <td>Female</td>
      <td>81</td>
      <td>0.14</td>
    </tr>
    <tr>
      <td>Other / Non-Disclosed</td>
      <td>11</td>
      <td>0.02</td>
    </tr>
  </tbody>
</table>
</div>




## Purchasing Analysis (Gender)

* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. by gender




* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python
#count of purchase by gender
purchase_count = gender_group["Purchase ID"]
#purchase_count

#average of the purchase by gender
avg_gender = gender_group["Price"].mean()


# #total purchase value
total_by_gender = gender_group["Price"].sum()



# #Avg Total Purchase per person
avg_total_purchase = total_by_gender/total_gender


sum_purch_gen_df = pd.DataFrame({"Purchase Count" : purchase_count, 
                          "Average Purchase Price" : avg_gender,
                           "Total Purchase Value" : total_by_gender,
                           "Average Total Purchase Per Person" : avg_total_purchase })

sum_purch_gen_df["Average Purchase Price"] = sum_purch_gen_df["Average Purchase Price"].map("{:,.2f}".format)
sum_purch_gen_df["Average Total Purchase Per Person"] = sum_purch_gen_df["Average Total Purchase Per Person"].map("{:,.2f}".format)
sum_purch_gen_df


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
      <th>Average Total Purchase Per Person</th>
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
      <td>Female</td>
      <td>113</td>
      <td>78.33</td>
      <td>235</td>
      <td>2.90</td>
    </tr>
    <tr>
      <td>Male</td>
      <td>652</td>
      <td>78.33</td>
      <td>235</td>
      <td>0.49</td>
    </tr>
    <tr>
      <td>Other / Non-Disclosed</td>
      <td>15</td>
      <td>78.33</td>
      <td>235</td>
      <td>21.36</td>
    </tr>
  </tbody>
</table>
</div>



## Age Demographics

* Establish bins for ages


* Categorize the existing players using the age bins. Hint: use pd.cut()


* Calculate the numbers and percentages by age group


* Create a summary data frame to hold the results


* Optional: round the percentage column to two decimal points


* Display Age Demographics Table



```python

```


```python
bins = [0.00,9.00,14.00,19.00,24.00,29.00,34.00,39.00,200]

labels = ["<10", "10-14","15-19","20-24", "25-29","30-34","35-39","40+"]

# Sort age values into bins use pd.cut
purchase_data["Age Group"] = pd.cut(purchase_data["Age"],bins, labels=labels)

# Create data frame of "Age Range" and group it
age_grp_df = purchase_data.groupby("Age Group")

# Count total players by age category
total_players_by_age = age_grp_df["SN"].nunique()
#total_players_by_age

# Calculate percentages by age category 
percent_by_age = total_players_by_age/total_players * 100
#percent_by_age

# Create data frame with obtained values
age_demo_df = pd.DataFrame({"Total Count": total_players_by_age, "Percentage of Players": percent_by_age})

#Add formatting
age_demo_df["Percentage of Players"] = age_demo_df["Percentage of Players"].map("{:,.2f}".format)
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
      <td>&lt;10</td>
      <td>17</td>
      <td>2.95</td>
    </tr>
    <tr>
      <td>10-14</td>
      <td>22</td>
      <td>3.82</td>
    </tr>
    <tr>
      <td>15-19</td>
      <td>107</td>
      <td>18.58</td>
    </tr>
    <tr>
      <td>20-24</td>
      <td>258</td>
      <td>44.79</td>
    </tr>
    <tr>
      <td>25-29</td>
      <td>77</td>
      <td>13.37</td>
    </tr>
    <tr>
      <td>30-34</td>
      <td>52</td>
      <td>9.03</td>
    </tr>
    <tr>
      <td>35-39</td>
      <td>31</td>
      <td>5.38</td>
    </tr>
    <tr>
      <td>40+</td>
      <td>12</td>
      <td>2.08</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Age)

* Bin the purchase_data data frame by age


* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. in the table below


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python
# Run basic calculations to obtain purchase count
age_purchase_count = age_grp_df["Purchase ID"].count()

#average purchase price
age_purchase_mean = age_grp_df["Price"].mean()

#total purchase value
age_purchase_total = age_grp_df["Price"].sum()

#average total price per person
age_avg_total_price = age_purchase_total/total_players_by_age

# Create data frame with obtained values
age_purchase_df = pd.DataFrame({"Purchase Count": age_purchase_count, 
                                "Average Purchase Price": age_purchase_mean,
                                "Total Purchase Value" : age_purchase_total,
                                   "Avg Total Purchase Per Person" : age_avg_total_price})
#Add formatting
age_purchase_df["Average Purchase Price"] = age_purchase_df["Average Purchase Price"].map("{:,.2f}".format)
age_purchase_df["Total Purchase Value"] = age_purchase_df["Total Purchase Value"].map("${:,.2f}".format)
age_purchase_df["Avg Total Purchase Per Person"] = age_purchase_df["Avg Total Purchase Per Person"].map("${:,.2f}".format)
age_purchase_df
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
      <th>Avg Total Purchase Per Person</th>
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
      <td>&lt;10</td>
      <td>23</td>
      <td>3.35</td>
      <td>$77.13</td>
      <td>$4.54</td>
    </tr>
    <tr>
      <td>10-14</td>
      <td>28</td>
      <td>2.96</td>
      <td>$82.78</td>
      <td>$3.76</td>
    </tr>
    <tr>
      <td>15-19</td>
      <td>136</td>
      <td>3.04</td>
      <td>$412.89</td>
      <td>$3.86</td>
    </tr>
    <tr>
      <td>20-24</td>
      <td>365</td>
      <td>3.05</td>
      <td>$1,114.06</td>
      <td>$4.32</td>
    </tr>
    <tr>
      <td>25-29</td>
      <td>101</td>
      <td>2.90</td>
      <td>$293.00</td>
      <td>$3.81</td>
    </tr>
    <tr>
      <td>30-34</td>
      <td>73</td>
      <td>2.93</td>
      <td>$214.00</td>
      <td>$4.12</td>
    </tr>
    <tr>
      <td>35-39</td>
      <td>41</td>
      <td>3.60</td>
      <td>$147.67</td>
      <td>$4.76</td>
    </tr>
    <tr>
      <td>40+</td>
      <td>13</td>
      <td>2.94</td>
      <td>$38.24</td>
      <td>$3.19</td>
    </tr>
  </tbody>
</table>
</div>



## Top Spenders

* Run basic calculations to obtain the results in the table below


* Create a summary data frame to hold the results


* Sort the total purchase value column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python
# Group purchase data by screen names
top_spender = purchase_data.groupby("SN")

# total purchases count by spender
count_purchase_spender = top_spender["Purchase ID"].count()

# average purchase 
avg_purchase_price_spender = top_spender["Price"].mean()

# Calculate purchase total 
purchase_total_spender = top_spender["Price"].sum()

# Create data frame with obtained values
top_summary = pd.DataFrame({"Purchase Count": count_purchase_spender,
                             "Average Purchase Price": avg_purchase_price_spender,
                             "Total Purchase Value":purchase_total_spender})
top_summary

# descending order 
top_summary = top_summary.sort_values(["Total Purchase Value"], ascending=False)

top_summary.head(5)
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
      <td>Lisosia93</td>
      <td>5</td>
      <td>3.792000</td>
      <td>18.96</td>
    </tr>
    <tr>
      <td>Idastidru52</td>
      <td>4</td>
      <td>3.862500</td>
      <td>15.45</td>
    </tr>
    <tr>
      <td>Chamjask73</td>
      <td>3</td>
      <td>4.610000</td>
      <td>13.83</td>
    </tr>
    <tr>
      <td>Iral74</td>
      <td>4</td>
      <td>3.405000</td>
      <td>13.62</td>
    </tr>
    <tr>
      <td>Iskadarya95</td>
      <td>3</td>
      <td>4.366667</td>
      <td>13.10</td>
    </tr>
  </tbody>
</table>
</div>



## Most Popular Items

* Retrieve the Item ID, Item Name, and Item Price columns


* Group by Item ID and Item Name. Perform calculations to obtain purchase count, item price, and total purchase value


* Create a summary data frame to hold the results


* Sort the purchase count column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python
# Retrieve the Item ID, Item Name, and Item Price columns
pop_df = purchase_data[["Item ID", "Item Name", "Price"]]

# Group by Item ID and Item Name 
item_id_name = pop_df.groupby(["Item ID","Item Name"])

# purchase count item
purchase_count_item = item_id_name["Price"].count()

# total purchase value per item 
purchase_value_item = item_id_name["Price"].sum()

# purchase item price
price_item = purchase_value_item/purchase_count_item

# Create data frame with obtained values
most_pop_item = pd.DataFrame({"Purchase Count": purchase_count_item, 
                                   "Item Price": price_item,
                                   "Total Purchase Value":purchase_value_item})
most_pop_item

# descending order 
most_pop_item = most_pop_item.sort_values(["Purchase Count"], ascending=False)

most_pop_item.head(5)
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
      <td>178</td>
      <td>Oathbreaker, Last Hope of the Breaking Storm</td>
      <td>12</td>
      <td>4.23</td>
      <td>50.76</td>
    </tr>
    <tr>
      <td>145</td>
      <td>Fiery Glass Crusader</td>
      <td>9</td>
      <td>4.58</td>
      <td>41.22</td>
    </tr>
    <tr>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>9</td>
      <td>3.53</td>
      <td>31.77</td>
    </tr>
    <tr>
      <td>82</td>
      <td>Nirvana</td>
      <td>9</td>
      <td>4.90</td>
      <td>44.10</td>
    </tr>
    <tr>
      <td>19</td>
      <td>Pursuit, Cudgel of Necromancy</td>
      <td>8</td>
      <td>1.02</td>
      <td>8.16</td>
    </tr>
  </tbody>
</table>
</div>



## Most Profitable Items

* Sort the above table by total purchase value in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the data frame




```python
most_pop_item = most_pop_item.sort_values(["Total Purchase Value"], ascending=False)

most_pop_item.head(5)
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
      <td>178</td>
      <td>Oathbreaker, Last Hope of the Breaking Storm</td>
      <td>12</td>
      <td>4.23</td>
      <td>50.76</td>
    </tr>
    <tr>
      <td>82</td>
      <td>Nirvana</td>
      <td>9</td>
      <td>4.90</td>
      <td>44.10</td>
    </tr>
    <tr>
      <td>145</td>
      <td>Fiery Glass Crusader</td>
      <td>9</td>
      <td>4.58</td>
      <td>41.22</td>
    </tr>
    <tr>
      <td>92</td>
      <td>Final Critic</td>
      <td>8</td>
      <td>4.88</td>
      <td>39.04</td>
    </tr>
    <tr>
      <td>103</td>
      <td>Singed Scalpel</td>
      <td>8</td>
      <td>4.35</td>
      <td>34.80</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
