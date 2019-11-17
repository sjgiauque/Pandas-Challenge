```python
# Dependencies and Setup
import pandas as pd

# File to Load (Remember to Change These)
file_to_load = "Resources/purchase_data.csv"

# Read Purchasing File and store into Pandas data frame
purchase_data = pd.read_csv(file_to_load)

```

## Player Count

* Display the total number of players



```python
# Define total players, use length of list of screen names "SN", count "SN" values in string
total_players = len(purchase_data["SN"].value_counts())

# Create data frame in order to return values (output/return is formatted)
player_count = pd.DataFrame({"Total Players":[total_players]})
player_count

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
# Capture unique items count (unique,) average price (mean,) purchase count (count,) and total revenue (sum)
unique_items = len((purchase_data["Item ID"]).unique())
average_price = (purchase_data["Price"]).mean()
purchase_count = (purchase_data["Purchase ID"]).count()
total_revenue = (purchase_data["Price"]).sum()

# Create data frame in order to return values (output/return is formatted)
summary_df = pd.DataFrame({"Number of Unique Items":[unique_items],
                           "Average Price":[average_price], 
                           "Number of Purchases": [purchase_count], 
                           "Total Revenue": [total_revenue]})

# Format average price & total revenue with $ currency and two significant figures
summary_df.style.format({'Average Price':"${:,.2f}",
                         'Total Revenue': '${:,.2f}'})

```




<style  type="text/css" >
</style><table id="T_0e11db8c_08e8_11ea_90fc_dca904867e7a" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Number of Unique Items</th>        <th class="col_heading level0 col1" >Average Price</th>        <th class="col_heading level0 col2" >Number of Purchases</th>        <th class="col_heading level0 col3" >Total Revenue</th>    </tr></thead><tbody>
                <tr>
                        <th id="T_0e11db8c_08e8_11ea_90fc_dca904867e7alevel0_row0" class="row_heading level0 row0" >0</th>
                        <td id="T_0e11db8c_08e8_11ea_90fc_dca904867e7arow0_col0" class="data row0 col0" >183</td>
                        <td id="T_0e11db8c_08e8_11ea_90fc_dca904867e7arow0_col1" class="data row0 col1" >$3.05</td>
                        <td id="T_0e11db8c_08e8_11ea_90fc_dca904867e7arow0_col2" class="data row0 col2" >780</td>
                        <td id="T_0e11db8c_08e8_11ea_90fc_dca904867e7arow0_col3" class="data row0 col3" >$2,379.77</td>
            </tr>
    </tbody></table>



## Gender Demographics

* Percentage and Count of Male Players


* Percentage and Count of Female Players


* Percentage and Count of Other / Non-Disclosed





```python
# Group purchase_data by gender (gouping)
gender_grouping = purchase_data.groupby("Gender")

# Count total screen names "SN" by gender (nunique)
count_by_gender = gender_grouping.nunique()["SN"]

# Calculate percentage by gender, divide count by gender by total players
percentage_by_gender = count_by_gender / total_players * 100

# Create data frame in order to return values (output/return is formatted)
gender_output = pd.DataFrame({"Total Count": count_by_gender, "Percentage of Players": percentage_by_gender})

# Format table by removing index name (0)
gender_output.index.name = None

# Sort by total count in descending order, add percentage with two significant figures
gender_output.sort_values(["Total Count"], ascending = False).style.format({"Percentage of Players":"{:.2f}%"})


```




<style  type="text/css" >
</style><table id="T_308f428a_08e8_11ea_90fc_dca904867e7a" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Total Count</th>        <th class="col_heading level0 col1" >Percentage of Players</th>    </tr></thead><tbody>
                <tr>
                        <th id="T_308f428a_08e8_11ea_90fc_dca904867e7alevel0_row0" class="row_heading level0 row0" >Male</th>
                        <td id="T_308f428a_08e8_11ea_90fc_dca904867e7arow0_col0" class="data row0 col0" >484</td>
                        <td id="T_308f428a_08e8_11ea_90fc_dca904867e7arow0_col1" class="data row0 col1" >84.03%</td>
            </tr>
            <tr>
                        <th id="T_308f428a_08e8_11ea_90fc_dca904867e7alevel0_row1" class="row_heading level0 row1" >Female</th>
                        <td id="T_308f428a_08e8_11ea_90fc_dca904867e7arow1_col0" class="data row1 col0" >81</td>
                        <td id="T_308f428a_08e8_11ea_90fc_dca904867e7arow1_col1" class="data row1 col1" >14.06%</td>
            </tr>
            <tr>
                        <th id="T_308f428a_08e8_11ea_90fc_dca904867e7alevel0_row2" class="row_heading level0 row2" >Other / Non-Disclosed</th>
                        <td id="T_308f428a_08e8_11ea_90fc_dca904867e7arow2_col0" class="data row2 col0" >11</td>
                        <td id="T_308f428a_08e8_11ea_90fc_dca904867e7arow2_col1" class="data row2 col1" >1.91%</td>
            </tr>
    </tbody></table>




## Purchasing Analysis (Gender)

* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. by gender




* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python
# Count total purchases by gender (count)
purchase_count = gender_stats["Purchase ID"].count()

# Calcuate average purchase price by gender (mean)
avg_purchase_price = gender_stats["Price"].mean()

# Calculate total purchase value by gender (sum)
total_purchase_value = gender_stats["Price"].sum()

# Calculate average total purchase per gender (total purchase value divided by count by gender)
avg_purchase_per_gender = total_purchase_value/count_by_gender

# Create data frame in order to return values (output/return is formatted)
gender_output = pd.DataFrame({"Purchase Count": purchase_count, 
                                    "Average Purchase Price": avg_purchase_price,
                                    "Total Purchase Value":total_purchase_value,
                                    "Avg Total Purchase per Person": avg_purchase_per_gender})

# Label top left index as "Gender" (replace 0 as index label)
gender_output.index.name = "Gender"

# Format average purchase price, total purchase value & avg total purchase/person with $ currency and two significant figures
gender_output.style.format({"Average Purchase Price":"${:,.2f}",
                                  "Total Purchase Value":"${:,.2f}",
                                  "Avg Total Purchase per Person":"${:,.2f}"})

```




<style  type="text/css" >
</style><table id="T_956fd3f8_08e9_11ea_90fc_dca904867e7a" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Purchase Count</th>        <th class="col_heading level0 col1" >Average Purchase Price</th>        <th class="col_heading level0 col2" >Total Purchase Value</th>        <th class="col_heading level0 col3" >Avg Total Purchase per Person</th>    </tr>    <tr>        <th class="index_name level0" >Gender</th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_956fd3f8_08e9_11ea_90fc_dca904867e7alevel0_row0" class="row_heading level0 row0" >Female</th>
                        <td id="T_956fd3f8_08e9_11ea_90fc_dca904867e7arow0_col0" class="data row0 col0" >113</td>
                        <td id="T_956fd3f8_08e9_11ea_90fc_dca904867e7arow0_col1" class="data row0 col1" >$3.20</td>
                        <td id="T_956fd3f8_08e9_11ea_90fc_dca904867e7arow0_col2" class="data row0 col2" >$361.94</td>
                        <td id="T_956fd3f8_08e9_11ea_90fc_dca904867e7arow0_col3" class="data row0 col3" >$4.47</td>
            </tr>
            <tr>
                        <th id="T_956fd3f8_08e9_11ea_90fc_dca904867e7alevel0_row1" class="row_heading level0 row1" >Male</th>
                        <td id="T_956fd3f8_08e9_11ea_90fc_dca904867e7arow1_col0" class="data row1 col0" >652</td>
                        <td id="T_956fd3f8_08e9_11ea_90fc_dca904867e7arow1_col1" class="data row1 col1" >$3.02</td>
                        <td id="T_956fd3f8_08e9_11ea_90fc_dca904867e7arow1_col2" class="data row1 col2" >$1,967.64</td>
                        <td id="T_956fd3f8_08e9_11ea_90fc_dca904867e7arow1_col3" class="data row1 col3" >$4.07</td>
            </tr>
            <tr>
                        <th id="T_956fd3f8_08e9_11ea_90fc_dca904867e7alevel0_row2" class="row_heading level0 row2" >Other / Non-Disclosed</th>
                        <td id="T_956fd3f8_08e9_11ea_90fc_dca904867e7arow2_col0" class="data row2 col0" >15</td>
                        <td id="T_956fd3f8_08e9_11ea_90fc_dca904867e7arow2_col1" class="data row2 col1" >$3.35</td>
                        <td id="T_956fd3f8_08e9_11ea_90fc_dca904867e7arow2_col2" class="data row2 col2" >$50.19</td>
                        <td id="T_956fd3f8_08e9_11ea_90fc_dca904867e7arow2_col3" class="data row2 col3" >$4.56</td>
            </tr>
    </tbody></table>



## Age Demographics

* Establish bins for ages


* Categorize the existing players using the age bins. Hint: use pd.cut()


* Calculate the numbers and percentages by age group


* Create a summary data frame to hold the results


* Optional: round the percentage column to two decimal points


* Display Age Demographics Table



```python
# Define bins for age segments and assign names
age_bins = [0, 9.99, 14.99, 19.99, 24.99, 29.99, 34.99, 39.99, 99999]
group_names = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"]

# Segment age values into corresponding bins
purchase_data["Age Group"] = pd.cut(purchase_data["Age"],age_bins, labels=group_names)
purchase_data

# Create data frame in order to return values (output/return is formatted)
# Group purchase_data by age ("Age Group") (gouping)
age_grouped = purchase_data.groupby("Age Group")

# Count total players by age (nunique) #Same as total screen names "SN" by gender
count_by_age = age_grouped["SN"].nunique()

# Calculate percentage by age category #Same as percentage by gender 
percentage_by_age = (count_by_age/total_players) * 100

# Create data frame in order to return values (output/return is formatted)
age_output = pd.DataFrame({"Total Count": count_by_age, "Percentage of Players": percentage_by_age})

# Format the data frame with no index name in the corner
age_output.index.name = None

# Format percentage with % and two decimal places 
age_output.style.format({"Percentage of Players":"{:,.2f}%"})

```




<style  type="text/css" >
</style><table id="T_c44d3238_08e9_11ea_90fc_dca904867e7a" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Total Count</th>        <th class="col_heading level0 col1" >Percentage of Players</th>    </tr></thead><tbody>
                <tr>
                        <th id="T_c44d3238_08e9_11ea_90fc_dca904867e7alevel0_row0" class="row_heading level0 row0" ><10</th>
                        <td id="T_c44d3238_08e9_11ea_90fc_dca904867e7arow0_col0" class="data row0 col0" >17</td>
                        <td id="T_c44d3238_08e9_11ea_90fc_dca904867e7arow0_col1" class="data row0 col1" >2.95%</td>
            </tr>
            <tr>
                        <th id="T_c44d3238_08e9_11ea_90fc_dca904867e7alevel0_row1" class="row_heading level0 row1" >10-14</th>
                        <td id="T_c44d3238_08e9_11ea_90fc_dca904867e7arow1_col0" class="data row1 col0" >22</td>
                        <td id="T_c44d3238_08e9_11ea_90fc_dca904867e7arow1_col1" class="data row1 col1" >3.82%</td>
            </tr>
            <tr>
                        <th id="T_c44d3238_08e9_11ea_90fc_dca904867e7alevel0_row2" class="row_heading level0 row2" >15-19</th>
                        <td id="T_c44d3238_08e9_11ea_90fc_dca904867e7arow2_col0" class="data row2 col0" >107</td>
                        <td id="T_c44d3238_08e9_11ea_90fc_dca904867e7arow2_col1" class="data row2 col1" >18.58%</td>
            </tr>
            <tr>
                        <th id="T_c44d3238_08e9_11ea_90fc_dca904867e7alevel0_row3" class="row_heading level0 row3" >20-24</th>
                        <td id="T_c44d3238_08e9_11ea_90fc_dca904867e7arow3_col0" class="data row3 col0" >258</td>
                        <td id="T_c44d3238_08e9_11ea_90fc_dca904867e7arow3_col1" class="data row3 col1" >44.79%</td>
            </tr>
            <tr>
                        <th id="T_c44d3238_08e9_11ea_90fc_dca904867e7alevel0_row4" class="row_heading level0 row4" >25-29</th>
                        <td id="T_c44d3238_08e9_11ea_90fc_dca904867e7arow4_col0" class="data row4 col0" >77</td>
                        <td id="T_c44d3238_08e9_11ea_90fc_dca904867e7arow4_col1" class="data row4 col1" >13.37%</td>
            </tr>
            <tr>
                        <th id="T_c44d3238_08e9_11ea_90fc_dca904867e7alevel0_row5" class="row_heading level0 row5" >30-34</th>
                        <td id="T_c44d3238_08e9_11ea_90fc_dca904867e7arow5_col0" class="data row5 col0" >52</td>
                        <td id="T_c44d3238_08e9_11ea_90fc_dca904867e7arow5_col1" class="data row5 col1" >9.03%</td>
            </tr>
            <tr>
                        <th id="T_c44d3238_08e9_11ea_90fc_dca904867e7alevel0_row6" class="row_heading level0 row6" >35-39</th>
                        <td id="T_c44d3238_08e9_11ea_90fc_dca904867e7arow6_col0" class="data row6 col0" >31</td>
                        <td id="T_c44d3238_08e9_11ea_90fc_dca904867e7arow6_col1" class="data row6 col1" >5.38%</td>
            </tr>
            <tr>
                        <th id="T_c44d3238_08e9_11ea_90fc_dca904867e7alevel0_row7" class="row_heading level0 row7" >40+</th>
                        <td id="T_c44d3238_08e9_11ea_90fc_dca904867e7arow7_col0" class="data row7 col0" >12</td>
                        <td id="T_c44d3238_08e9_11ea_90fc_dca904867e7arow7_col1" class="data row7 col1" >2.08%</td>
            </tr>
    </tbody></table>



## Purchasing Analysis (Age)

* Bin the purchase_data data frame by age


* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. in the table below


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python
# Count total purchases by age group (count)
purchase_count_age = age_grouped["Purchase ID"].count()

# Calculate average purchase price by age group (mean)
avg_purchase_price_age = age_grouped["Price"].mean()

# Calculate total purchase value by age group (sum)
total_purchase_value = age_grouped["Price"].sum()

# Calculate average total purchase per person in the age group (total purchase value divided by total count age)
avg_purchase_by_age = total_purchase_value/total_count_age

# Create data frame in order to return values (output/return is formatted)
age_output = pd.DataFrame({"Purchase Count": purchase_count_age,
                                 "Average Purchase Price": avg_purchase_price_age,
                                 "Total Purchase Value":total_purchase_value,
                                 "Avg Total Purchase per Person": avg_purchase_by_age})

# Format the data frame with no index name in the corner
age_output.index.name = None

# Format with currency style
age_output.style.format({"Average Purchase Price":"${:,.2f}",
                               "Total Purchase Value":"${:,.2f}",
                               "Avg Total Purchase per Person":"${:,.2f}"})


```




<style  type="text/css" >
</style><table id="T_e125d716_08e9_11ea_90fc_dca904867e7a" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Purchase Count</th>        <th class="col_heading level0 col1" >Average Purchase Price</th>        <th class="col_heading level0 col2" >Total Purchase Value</th>        <th class="col_heading level0 col3" >Avg Total Purchase per Person</th>    </tr></thead><tbody>
                <tr>
                        <th id="T_e125d716_08e9_11ea_90fc_dca904867e7alevel0_row0" class="row_heading level0 row0" ><10</th>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow0_col0" class="data row0 col0" >23</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow0_col1" class="data row0 col1" >$3.35</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow0_col2" class="data row0 col2" >$77.13</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow0_col3" class="data row0 col3" >$4.54</td>
            </tr>
            <tr>
                        <th id="T_e125d716_08e9_11ea_90fc_dca904867e7alevel0_row1" class="row_heading level0 row1" >10-14</th>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow1_col0" class="data row1 col0" >28</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow1_col1" class="data row1 col1" >$2.96</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow1_col2" class="data row1 col2" >$82.78</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow1_col3" class="data row1 col3" >$3.76</td>
            </tr>
            <tr>
                        <th id="T_e125d716_08e9_11ea_90fc_dca904867e7alevel0_row2" class="row_heading level0 row2" >15-19</th>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow2_col0" class="data row2 col0" >136</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow2_col1" class="data row2 col1" >$3.04</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow2_col2" class="data row2 col2" >$412.89</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow2_col3" class="data row2 col3" >$3.86</td>
            </tr>
            <tr>
                        <th id="T_e125d716_08e9_11ea_90fc_dca904867e7alevel0_row3" class="row_heading level0 row3" >20-24</th>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow3_col0" class="data row3 col0" >365</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow3_col1" class="data row3 col1" >$3.05</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow3_col2" class="data row3 col2" >$1,114.06</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow3_col3" class="data row3 col3" >$4.32</td>
            </tr>
            <tr>
                        <th id="T_e125d716_08e9_11ea_90fc_dca904867e7alevel0_row4" class="row_heading level0 row4" >25-29</th>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow4_col0" class="data row4 col0" >101</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow4_col1" class="data row4 col1" >$2.90</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow4_col2" class="data row4 col2" >$293.00</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow4_col3" class="data row4 col3" >$3.81</td>
            </tr>
            <tr>
                        <th id="T_e125d716_08e9_11ea_90fc_dca904867e7alevel0_row5" class="row_heading level0 row5" >30-34</th>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow5_col0" class="data row5 col0" >73</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow5_col1" class="data row5 col1" >$2.93</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow5_col2" class="data row5 col2" >$214.00</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow5_col3" class="data row5 col3" >$4.12</td>
            </tr>
            <tr>
                        <th id="T_e125d716_08e9_11ea_90fc_dca904867e7alevel0_row6" class="row_heading level0 row6" >35-39</th>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow6_col0" class="data row6 col0" >41</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow6_col1" class="data row6 col1" >$3.60</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow6_col2" class="data row6 col2" >$147.67</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow6_col3" class="data row6 col3" >$4.76</td>
            </tr>
            <tr>
                        <th id="T_e125d716_08e9_11ea_90fc_dca904867e7alevel0_row7" class="row_heading level0 row7" >40+</th>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow7_col0" class="data row7 col0" >13</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow7_col1" class="data row7 col1" >$2.94</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow7_col2" class="data row7 col2" >$38.24</td>
                        <td id="T_e125d716_08e9_11ea_90fc_dca904867e7arow7_col3" class="data row7 col3" >$3.19</td>
            </tr>
    </tbody></table>



## Top Spenders

* Run basic calculations to obtain the results in the table below


* Create a summary data frame to hold the results


* Sort the total purchase value column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python
# Identify top 5 spenders by purchase count, avg purchase price, total purchase value
# Replicate the same code as was done for gender and age groups

# Group purchase_data by screen names (gouping)
spender_stats = purchase_data.groupby("SN")

# Count total purchases by spender (count)
purchase_count_by_spender = spender_stats["Purchase ID"].count()

# Calcuate average purchase price by spender (mean)
avg_purchase_price_spender = spender_stats["Price"].mean()

# Calculate total purchase value by spender (sum)
purchase_total_spender = spender_stats["Price"].sum()

# Create data frame in order to return values (output/return is formatted)
top_spenders = pd.DataFrame({"Purchase Count": purchase_count_by_spender,
                             "Average Purchase Price": avg_purchase_price_spender,
                             "Total Purchase Value":purchase_total_spender})

# Sort in descending order to obtain top 5 spender names, print head
formatted_spenders = top_spenders.sort_values(["Total Purchase Value"], ascending=False).head()

# Format table by assigning "SN" as index name
formatted_spenders.index.name = "SN"

# Format average purchase price & total purchase value with $ currency and two significant figures
formatted_spenders.style.format({"Average Purchase Price":"${:,.2f}", 
                                 "Total Purchase Value":"${:,.2f}"})

```




<style  type="text/css" >
</style><table id="T_b99aa796_08e2_11ea_90fc_dca904867e7a" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Purchase Count</th>        <th class="col_heading level0 col1" >Average Purchase Price</th>        <th class="col_heading level0 col2" >Total Purchase Value</th>    </tr>    <tr>        <th class="index_name level0" >SN</th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_b99aa796_08e2_11ea_90fc_dca904867e7alevel0_row0" class="row_heading level0 row0" >Lisosia93</th>
                        <td id="T_b99aa796_08e2_11ea_90fc_dca904867e7arow0_col0" class="data row0 col0" >5</td>
                        <td id="T_b99aa796_08e2_11ea_90fc_dca904867e7arow0_col1" class="data row0 col1" >$3.79</td>
                        <td id="T_b99aa796_08e2_11ea_90fc_dca904867e7arow0_col2" class="data row0 col2" >$18.96</td>
            </tr>
            <tr>
                        <th id="T_b99aa796_08e2_11ea_90fc_dca904867e7alevel0_row1" class="row_heading level0 row1" >Idastidru52</th>
                        <td id="T_b99aa796_08e2_11ea_90fc_dca904867e7arow1_col0" class="data row1 col0" >4</td>
                        <td id="T_b99aa796_08e2_11ea_90fc_dca904867e7arow1_col1" class="data row1 col1" >$3.86</td>
                        <td id="T_b99aa796_08e2_11ea_90fc_dca904867e7arow1_col2" class="data row1 col2" >$15.45</td>
            </tr>
            <tr>
                        <th id="T_b99aa796_08e2_11ea_90fc_dca904867e7alevel0_row2" class="row_heading level0 row2" >Chamjask73</th>
                        <td id="T_b99aa796_08e2_11ea_90fc_dca904867e7arow2_col0" class="data row2 col0" >3</td>
                        <td id="T_b99aa796_08e2_11ea_90fc_dca904867e7arow2_col1" class="data row2 col1" >$4.61</td>
                        <td id="T_b99aa796_08e2_11ea_90fc_dca904867e7arow2_col2" class="data row2 col2" >$13.83</td>
            </tr>
            <tr>
                        <th id="T_b99aa796_08e2_11ea_90fc_dca904867e7alevel0_row3" class="row_heading level0 row3" >Iral74</th>
                        <td id="T_b99aa796_08e2_11ea_90fc_dca904867e7arow3_col0" class="data row3 col0" >4</td>
                        <td id="T_b99aa796_08e2_11ea_90fc_dca904867e7arow3_col1" class="data row3 col1" >$3.40</td>
                        <td id="T_b99aa796_08e2_11ea_90fc_dca904867e7arow3_col2" class="data row3 col2" >$13.62</td>
            </tr>
            <tr>
                        <th id="T_b99aa796_08e2_11ea_90fc_dca904867e7alevel0_row4" class="row_heading level0 row4" >Iskadarya95</th>
                        <td id="T_b99aa796_08e2_11ea_90fc_dca904867e7arow4_col0" class="data row4 col0" >3</td>
                        <td id="T_b99aa796_08e2_11ea_90fc_dca904867e7arow4_col1" class="data row4 col1" >$4.37</td>
                        <td id="T_b99aa796_08e2_11ea_90fc_dca904867e7arow4_col2" class="data row4 col2" >$13.10</td>
            </tr>
    </tbody></table>



## Most Popular Items

* Retrieve the Item ID, Item Name, and Item Price columns


* Group by Item ID and Item Name. Perform calculations to obtain purchase count, item price, and total purchase value


* Create a summary data frame to hold the results


* Sort the purchase count column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python
# Identify top 5 items by purchase count, sorting by Item ID, item name, item price, and total purchase value
# Replicate the same code as was done for gender, age groups, and top spenders

# Create new data frame capturing relevent sort categories
items = purchase_data[["Item ID", "Item Name", "Price"]]

# Group the item data by item id and item name 
item_stats = items.groupby(["Item ID","Item Name"])

# Count total purchases by item, grouped 1:1 by both item id and item name (count)
purchase_count_item = item_stats["Price"].count()

# Calculate total purchase value by item (sum)
purchase_value_item = (item_stats["Price"].sum()) 

# Calculate individual item price (total purchase value divided by purchase count)
item_price = purchase_value_item/purchase_count_item

# Create data frame in order to return values (output/return is formatted)
most_popular_items = pd.DataFrame({"Purchase Count": purchase_count_item, 
                                   "Item Price": item_price,
                                   "Total Purchase Value":purchase_value_item})

# Sort in descending order top 5 item names by purchase count, print head
popular_formatted = most_popular_items.sort_values(["Purchase Count"], ascending=False).head()

# Format item price and total purchase value with $ currency and two significant figures
popular_formatted.style.format({"Item Price":"${:,.2f}",
                                "Total Purchase Value":"${:,.2f}"})

```




<style  type="text/css" >
</style><table id="T_b58087b4_08e4_11ea_90fc_dca904867e7a" ><thead>    <tr>        <th class="blank" ></th>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Purchase Count</th>        <th class="col_heading level0 col1" >Item Price</th>        <th class="col_heading level0 col2" >Total Purchase Value</th>    </tr>    <tr>        <th class="index_name level0" >Item ID</th>        <th class="index_name level1" >Item Name</th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_b58087b4_08e4_11ea_90fc_dca904867e7alevel0_row0" class="row_heading level0 row0" >178</th>
                        <th id="T_b58087b4_08e4_11ea_90fc_dca904867e7alevel1_row0" class="row_heading level1 row0" >Oathbreaker, Last Hope of the Breaking Storm</th>
                        <td id="T_b58087b4_08e4_11ea_90fc_dca904867e7arow0_col0" class="data row0 col0" >12</td>
                        <td id="T_b58087b4_08e4_11ea_90fc_dca904867e7arow0_col1" class="data row0 col1" >$4.23</td>
                        <td id="T_b58087b4_08e4_11ea_90fc_dca904867e7arow0_col2" class="data row0 col2" >$50.76</td>
            </tr>
            <tr>
                        <th id="T_b58087b4_08e4_11ea_90fc_dca904867e7alevel0_row1" class="row_heading level0 row1" >145</th>
                        <th id="T_b58087b4_08e4_11ea_90fc_dca904867e7alevel1_row1" class="row_heading level1 row1" >Fiery Glass Crusader</th>
                        <td id="T_b58087b4_08e4_11ea_90fc_dca904867e7arow1_col0" class="data row1 col0" >9</td>
                        <td id="T_b58087b4_08e4_11ea_90fc_dca904867e7arow1_col1" class="data row1 col1" >$4.58</td>
                        <td id="T_b58087b4_08e4_11ea_90fc_dca904867e7arow1_col2" class="data row1 col2" >$41.22</td>
            </tr>
            <tr>
                        <th id="T_b58087b4_08e4_11ea_90fc_dca904867e7alevel0_row2" class="row_heading level0 row2" >108</th>
                        <th id="T_b58087b4_08e4_11ea_90fc_dca904867e7alevel1_row2" class="row_heading level1 row2" >Extraction, Quickblade Of Trembling Hands</th>
                        <td id="T_b58087b4_08e4_11ea_90fc_dca904867e7arow2_col0" class="data row2 col0" >9</td>
                        <td id="T_b58087b4_08e4_11ea_90fc_dca904867e7arow2_col1" class="data row2 col1" >$3.53</td>
                        <td id="T_b58087b4_08e4_11ea_90fc_dca904867e7arow2_col2" class="data row2 col2" >$31.77</td>
            </tr>
            <tr>
                        <th id="T_b58087b4_08e4_11ea_90fc_dca904867e7alevel0_row3" class="row_heading level0 row3" >82</th>
                        <th id="T_b58087b4_08e4_11ea_90fc_dca904867e7alevel1_row3" class="row_heading level1 row3" >Nirvana</th>
                        <td id="T_b58087b4_08e4_11ea_90fc_dca904867e7arow3_col0" class="data row3 col0" >9</td>
                        <td id="T_b58087b4_08e4_11ea_90fc_dca904867e7arow3_col1" class="data row3 col1" >$4.90</td>
                        <td id="T_b58087b4_08e4_11ea_90fc_dca904867e7arow3_col2" class="data row3 col2" >$44.10</td>
            </tr>
            <tr>
                        <th id="T_b58087b4_08e4_11ea_90fc_dca904867e7alevel0_row4" class="row_heading level0 row4" >19</th>
                        <th id="T_b58087b4_08e4_11ea_90fc_dca904867e7alevel1_row4" class="row_heading level1 row4" >Pursuit, Cudgel of Necromancy</th>
                        <td id="T_b58087b4_08e4_11ea_90fc_dca904867e7arow4_col0" class="data row4 col0" >8</td>
                        <td id="T_b58087b4_08e4_11ea_90fc_dca904867e7arow4_col1" class="data row4 col1" >$1.02</td>
                        <td id="T_b58087b4_08e4_11ea_90fc_dca904867e7arow4_col2" class="data row4 col2" >$8.16</td>
            </tr>
    </tbody></table>



## Most Profitable Items

* Sort the above table by total purchase value in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the data frame




```python
# Identify top 5 items by total purchase value, sorting by Item ID, item name, purchase count, and item price
# Replicate the same code as was done for top 5 items by purchase count

# Sort in descending order top 5 item names by total purchase value, print head
popular_formatted = most_popular_items.sort_values(["Total Purchase Value"],
                                                   ascending=False).head()
# Format item price and total purchase value with $ currency and two significant figures
popular_formatted.style.format({"Item Price":"${:,.2f}",
                                "Total Purchase Value":"${:,.2f}"})

```




<style  type="text/css" >
</style><table id="T_9e07048a_08e6_11ea_90fc_dca904867e7a" ><thead>    <tr>        <th class="blank" ></th>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Purchase Count</th>        <th class="col_heading level0 col1" >Item Price</th>        <th class="col_heading level0 col2" >Total Purchase Value</th>    </tr>    <tr>        <th class="index_name level0" >Item ID</th>        <th class="index_name level1" >Item Name</th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_9e07048a_08e6_11ea_90fc_dca904867e7alevel0_row0" class="row_heading level0 row0" >178</th>
                        <th id="T_9e07048a_08e6_11ea_90fc_dca904867e7alevel1_row0" class="row_heading level1 row0" >Oathbreaker, Last Hope of the Breaking Storm</th>
                        <td id="T_9e07048a_08e6_11ea_90fc_dca904867e7arow0_col0" class="data row0 col0" >12</td>
                        <td id="T_9e07048a_08e6_11ea_90fc_dca904867e7arow0_col1" class="data row0 col1" >$4.23</td>
                        <td id="T_9e07048a_08e6_11ea_90fc_dca904867e7arow0_col2" class="data row0 col2" >$50.76</td>
            </tr>
            <tr>
                        <th id="T_9e07048a_08e6_11ea_90fc_dca904867e7alevel0_row1" class="row_heading level0 row1" >82</th>
                        <th id="T_9e07048a_08e6_11ea_90fc_dca904867e7alevel1_row1" class="row_heading level1 row1" >Nirvana</th>
                        <td id="T_9e07048a_08e6_11ea_90fc_dca904867e7arow1_col0" class="data row1 col0" >9</td>
                        <td id="T_9e07048a_08e6_11ea_90fc_dca904867e7arow1_col1" class="data row1 col1" >$4.90</td>
                        <td id="T_9e07048a_08e6_11ea_90fc_dca904867e7arow1_col2" class="data row1 col2" >$44.10</td>
            </tr>
            <tr>
                        <th id="T_9e07048a_08e6_11ea_90fc_dca904867e7alevel0_row2" class="row_heading level0 row2" >145</th>
                        <th id="T_9e07048a_08e6_11ea_90fc_dca904867e7alevel1_row2" class="row_heading level1 row2" >Fiery Glass Crusader</th>
                        <td id="T_9e07048a_08e6_11ea_90fc_dca904867e7arow2_col0" class="data row2 col0" >9</td>
                        <td id="T_9e07048a_08e6_11ea_90fc_dca904867e7arow2_col1" class="data row2 col1" >$4.58</td>
                        <td id="T_9e07048a_08e6_11ea_90fc_dca904867e7arow2_col2" class="data row2 col2" >$41.22</td>
            </tr>
            <tr>
                        <th id="T_9e07048a_08e6_11ea_90fc_dca904867e7alevel0_row3" class="row_heading level0 row3" >92</th>
                        <th id="T_9e07048a_08e6_11ea_90fc_dca904867e7alevel1_row3" class="row_heading level1 row3" >Final Critic</th>
                        <td id="T_9e07048a_08e6_11ea_90fc_dca904867e7arow3_col0" class="data row3 col0" >8</td>
                        <td id="T_9e07048a_08e6_11ea_90fc_dca904867e7arow3_col1" class="data row3 col1" >$4.88</td>
                        <td id="T_9e07048a_08e6_11ea_90fc_dca904867e7arow3_col2" class="data row3 col2" >$39.04</td>
            </tr>
            <tr>
                        <th id="T_9e07048a_08e6_11ea_90fc_dca904867e7alevel0_row4" class="row_heading level0 row4" >103</th>
                        <th id="T_9e07048a_08e6_11ea_90fc_dca904867e7alevel1_row4" class="row_heading level1 row4" >Singed Scalpel</th>
                        <td id="T_9e07048a_08e6_11ea_90fc_dca904867e7arow4_col0" class="data row4 col0" >8</td>
                        <td id="T_9e07048a_08e6_11ea_90fc_dca904867e7arow4_col1" class="data row4 col1" >$4.35</td>
                        <td id="T_9e07048a_08e6_11ea_90fc_dca904867e7arow4_col2" class="data row4 col2" >$34.80</td>
            </tr>
    </tbody></table>




```python

```
