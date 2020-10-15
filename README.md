# Pandas Homework - Pandas, Pandas, Pandas

## Background

The data dive continues!

Now, it's time to take what you've learned about Python Pandas and apply it to new situations. For this assignment, you'll need to complete **one of two** (not both)  Data Challenges. Once again, which challenge you take on is your choice. Just be sure to give it your all -- as the skills you hone will become powerful tools in your data analytics tool belt.

### Before You Begin

1. Create a new repository for this project called `pandas-challenge`. **Do not add this homework to an existing repository**.

2. Clone the new repository to your computer.

3. Inside your local git repository, create a directory for the Pandas Challenge you choose. Use folder names corresponding to the challenges: **HeroesOfPymoli** or  **PyCitySchools**.

4. Add your Jupyter notebook to this folder. This will be the main script to run for analysis.

5. Push the above changes to GitHub or GitLab.

## Option 1: Heroes of Pymoli

![Fantasy](Images/Fantasy.png)

Congratulations! After a lot of hard work in the data munging mines, you've landed a job as Lead Analyst for an independent gaming company. You've been assigned the task of analyzing the data for their most recent fantasy game Heroes of Pymoli.

Like many others in its genre, the game is free-to-play, but players are encouraged to purchase optional items that enhance their playing experience. As a first task, the company would like you to generate a report that breaks down the game's purchasing data into meaningful insights.

Your final report should include each of the following:


 ```python 
 
# Dependencies and Setup
import pandas as pd
file_to_load = "Resources/purchase_data.csv"

# Read Purchasing File and store into Pandas data frame
 purchase_data = pd.read_csv(file_to_load)
```

### Player Count

* Total Number of Players
```
total_players = len(purchase_data['SN'].value_counts())
players_count = pd.DataFrame([total_players])
players_count
```

<div>

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

### Purchasing Analysis (Total)

* Number of Unique Items
* Average Purchase Price
* Total Number of Purchases
* Total Revenue
```
Number_of_Unique_Items = len(purchase_data['Item Name'].unique())
Average_Price = purchase_data['Price'].mean()
Number_of_Purchases = purchase_data['Purchase ID'].count()
Total_Revenue = purchase_data['Price'].sum()

# Create a Summary Dataframe

purchase_summary = pd.DataFrame([{'Number of Unique Items':Number_of_Unique_Items,
                                'Average Price':Average_Price,
                                'Number of Purchases':Number_of_Purchases,
                                'Total Revenue':Total_Revenue}])

# purchase_summary.style.format({'Average Price':"${:,.2f}",'Total Revenue':"${:,.2f}"})

purchase_summary['Average Price']=purchase_summary['Average Price'].astype(float).map("${:,.2f}".format)
purchase_summary['Total Revenue']=purchase_summary['Total Revenue'].astype(float).map("${:,.2f}".format)

```

<table id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630f" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Number of Unique Items</th> 
        <th class="col_heading level0 col1" >Average Price</th> 
        <th class="col_heading level0 col2" >Number of Purchases</th> 
        <th class="col_heading level0 col3" >Total Revenue</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row0" >0</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >179</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >$3.05</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >780</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$2,379.77</td> 
    </tr></tbody> 
</table> 


### Gender Demographics

* Percentage and Count of Male Players
* Percentage and Count of Female Players
* Percentage and Count of Other / Non-Disclosed

```
# Identify Unique Records using column 'SN'

purchase_data_unique = purchase_data.drop_duplicates('SN')
purchase_data_unique.head()

# Identify gender counts

total_gender = purchase_data_unique['Gender'].value_counts()
total_gender

# calculate percentage

Percentage_of_Players = total_gender/total_players * 100
Percentage_of_Players

# create a summary data frame
gender_demographics = pd.DataFrame({'Total Count':total_gender,'Percentage of Players':Percentage_of_Players})

# format the Percetage field

gender_demographics['Percentage of Players'] = gender_demographics['Percentage of Players'].astype(float).map("{:,.2f}%".format)

```

<table id="T_8ec2dd4c_9c53_11e8_8bab_d49a20d1630f" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Total Count</th> 
        <th class="col_heading level0 col1" >Percentage of Players</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_8ec2dd4c_9c53_11e8_8bab_d49a20d1630flevel0_row0" class="row_heading level0 row0" >Male</th> 
        <td id="T_8ec2dd4c_9c53_11e8_8bab_d49a20d1630frow0_col0" class="data row0 col1" >484</td> 
        <td id="T_8ec2dd4c_9c53_11e8_8bab_d49a20d1630frow0_col1" class="data row0 col0" >84.03%</td> 
    </tr>    <tr> 
        <th id="T_8ec2dd4c_9c53_11e8_8bab_d49a20d1630flevel0_row1" class="row_heading level0 row1" >Female</th> 
        <td id="T_8ec2dd4c_9c53_11e8_8bab_d49a20d1630frow1_col0" class="data row1 col1" >81</td> 
        <td id="T_8ec2dd4c_9c53_11e8_8bab_d49a20d1630frow1_col1" class="data row1 col0" >14.06%</td> 
    </tr>    <tr> 
        <th id="T_8ec2dd4c_9c53_11e8_8bab_d49a20d1630flevel0_row2" class="row_heading level0 row2" >Other / Non-Disclosed</th> 
        <td id="T_8ec2dd4c_9c53_11e8_8bab_d49a20d1630frow2_col0" class="data row2 col1" >11</td> 
        <td id="T_8ec2dd4c_9c53_11e8_8bab_d49a20d1630frow2_col1" class="data row2 col0" >1.91%</td> 
    </tr></tbody> 
</table> 

### Purchasing Analysis (Gender)

* The below each broken by gender
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value
  * Average Purchase Total per Person by Gender

```python
# calculate purchase count by 'GENDER'

Purchase_Count = purchase_data['Gender'].value_counts()

# Calculate Average Purchase price by 'GENDER'

Average_Purchase_Price = purchase_data.groupby('Gender')['Price'].mean()

# Calculate total purchase value by 'GENDER'

Total_Purchase_Value = purchase_data.groupby('Gender')['Price'].sum()

# Calculate Avg total purchange per person

Avg_Total_Purchase_per_Person = Total_Purchase_Value/total_gender

# create a summary dataframe

purchasing_analysis_summary = pd.DataFrame({
    'Purchase Count':Purchase_Count,
    'Average Purchase Price':Average_Purchase_Price,
    'Total Purchase Value': Total_Purchase_Value,
    'Avg Total Purchase per Person':Avg_Total_Purchase_per_Person
})

# Format the price columns

purchasing_analysis_summary['Average Purchase Price'] = purchasing_analysis_summary['Average Purchase Price'].astype(float).map("${:,.2f}".format)
purchasing_analysis_summary['Total Purchase Value'] = purchasing_analysis_summary['Total Purchase Value'].astype(float).map("${:,.2f}".format)
purchasing_analysis_summary['Avg Total Purchase per Person'] = purchasing_analysis_summary['Avg Total Purchase per Person'].astype(float).map("${:,.2f}".format)

```

<table id="T_8ec591b8_9c53_11e8_885f_d49a20d1630f" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Purchase Count</th> 
        <th class="col_heading level0 col1" >Average Purchase Price</th> 
        <th class="col_heading level0 col2" >Total Purchase Value</th> 
        <th class="col_heading level0 col3" >Avg Total Purchase per Person</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Gender</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_8ec591b8_9c53_11e8_885f_d49a20d1630flevel0_row0" class="row_heading level0 row0" >Female</th> 
        <td id="T_8ec591b8_9c53_11e8_885f_d49a20d1630frow0_col0" class="data row0 col0" >113</td> 
        <td id="T_8ec591b8_9c53_11e8_885f_d49a20d1630frow0_col1" class="data row0 col1" >$3.20</td> 
        <td id="T_8ec591b8_9c53_11e8_885f_d49a20d1630frow0_col2" class="data row0 col2" >$361.94</td> 
        <td id="T_8ec591b8_9c53_11e8_885f_d49a20d1630frow0_col3" class="data row0 col3" >$4.47</td> 
    </tr>    <tr> 
        <th id="T_8ec591b8_9c53_11e8_885f_d49a20d1630flevel0_row1" class="row_heading level0 row1" >Male</th> 
        <td id="T_8ec591b8_9c53_11e8_885f_d49a20d1630frow1_col0" class="data row1 col0" >652</td> 
        <td id="T_8ec591b8_9c53_11e8_885f_d49a20d1630frow1_col1" class="data row1 col1" >$3.02</td> 
        <td id="T_8ec591b8_9c53_11e8_885f_d49a20d1630frow1_col2" class="data row1 col2" >$1,967.64</td> 
        <td id="T_8ec591b8_9c53_11e8_885f_d49a20d1630frow1_col3" class="data row1 col3" >$4.07</td> 
    </tr>    <tr> 
        <th id="T_8ec591b8_9c53_11e8_885f_d49a20d1630flevel0_row2" class="row_heading level0 row2" >Other / Non-Disclosed</th> 
        <td id="T_8ec591b8_9c53_11e8_885f_d49a20d1630frow2_col0" class="data row2 col0" >15</td> 
        <td id="T_8ec591b8_9c53_11e8_885f_d49a20d1630frow2_col1" class="data row2 col1" >$3.35</td> 
        <td id="T_8ec591b8_9c53_11e8_885f_d49a20d1630frow2_col2" class="data row2 col2" >$50.19</td> 
        <td id="T_8ec591b8_9c53_11e8_885f_d49a20d1630frow2_col3" class="data row2 col3" >$4.56</td> 
    </tr></tbody> 
</table> 


### Age Demographics

* The below each broken into bins of 4 years (i.e. &lt;10, 10-14, 15-19, etc.)
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value
  * Average Purchase Total per Person by Age Group
 
 ```python
 
#create bins and labels & Categorize the existing players using the age bins. Hint: use pd.cut()

bins = [0,9.99,14.99,19.99,24.99,29.99,34.99,39.99,199]
group_names = ['<10','10-14','15-19','20-24','25-29','30-34','35-39','40+']

pd.cut(purchase_data['Age'],bins,labels=group_names,include_lowest=True)

# now add a new column Age Group to the exisitng DF with and assign pd.cut() value

purchase_data['Age Group'] = pd.cut(purchase_data['Age'],bins,labels=group_names,include_lowest=True)

# create a new field with new column Age Group

group_aged = purchase_data.groupby('Age Group')

# Count distinct observations over requested axis/column.

unique_age_totals = group_aged['SN'].nunique()

# calculate Percentage of Players

Percentage_of_Players = unique_age_totals/total_players * 100

# create a new DF with summary

age_summary = pd.DataFrame({
    'Total Count': unique_age_totals,
    'Percentage of Players': Percentage_of_Players
})

# Format Percentqage column
age_summary['Percentage of Players'] = age_summary['Percentage of Players'].astype(float).map("{:,.2f}%".format)

# Remove Index name 
age_summary.index.name=None
 ```

 
<table id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630f" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Total Count</th> 
        <th class="col_heading level0 col1" >Percentage of Players</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630flevel0_row0" class="row_heading level0 row0" ><10</th> 
        <td id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630frow0_col0" class="data row0 col0" >17</td> 
        <td id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630frow0_col1" class="data row0 col1" >2.95%</td> 
    </tr>    <tr> 
        <th id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630flevel0_row1" class="row_heading level0 row1" >10-14</th> 
        <td id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630frow1_col0" class="data row1 col0" >22</td> 
        <td id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630frow1_col1" class="data row1 col1" >3.82%</td> 
    </tr>    <tr> 
        <th id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630flevel0_row2" class="row_heading level0 row2" >15-19</th> 
        <td id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630frow2_col0" class="data row2 col0" >107</td> 
        <td id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630frow2_col1" class="data row2 col1" >18.58%</td> 
    </tr>    <tr> 
        <th id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630flevel0_row3" class="row_heading level0 row3" >20-24</th> 
        <td id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630frow3_col0" class="data row3 col0" >258</td> 
        <td id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630frow3_col1" class="data row3 col1" >44.79%</td> 
    </tr>    <tr> 
        <th id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630flevel0_row4" class="row_heading level0 row4" >25-29</th> 
        <td id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630frow4_col0" class="data row4 col0" >77</td> 
        <td id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630frow4_col1" class="data row4 col1" >13.37%</td> 
    </tr>    <tr> 
        <th id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630flevel0_row5" class="row_heading level0 row5" >30-34</th> 
        <td id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630frow5_col0" class="data row5 col0" >52</td> 
        <td id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630frow5_col1" class="data row5 col1" >9.03%</td> 
    </tr>    <tr> 
        <th id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630flevel0_row6" class="row_heading level0 row6" >35-39</th> 
        <td id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630frow6_col0" class="data row6 col0" >31</td> 
        <td id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630frow6_col1" class="data row6 col1" >5.38%</td> 
    </tr>    <tr> 
        <th id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630flevel0_row7" class="row_heading level0 row7" >40+</th> 
        <td id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630frow7_col0" class="data row7 col0" >12</td> 
        <td id="T_8ec9961e_9c53_11e8_9e37_d49a20d1630frow7_col1" class="data row7 col1" >2.08%</td> 
    </tr></tbody> 
</table> 

### Purchasing Analysis (Age)
 * Bin the purchase_data data frame by age
 * Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. in the table below
 * Create a summary data frame to hold the results
 * Optional: give the displayed data cleaner formatting
 * Display the summary data frame
 
```python
# Calculate purchase_count_by_age_group
purchase_count_by_age_group = purchase_data['Age Group'].value_counts()

# Calculate avg_price_purchange_by_age_group
avg_price_purchange_by_age_group = purchase_data.groupby('Age Group')['Price'].mean()

# Calculate Total_purchase_value_by_age_group
Total_purchase_value_by_age_group = purchase_data.groupby('Age Group')['Price'].sum()

# Calculate Avg_Total_Purchase_per_Person_by_age_group
Avg_Total_Purchase_per_Person_by_age_group = Total_purchase_value_by_age_group/unique_age_totals

Purchasing_Analysis_Summary = pd.DataFrame({
    'Purchase Count': purchase_count_by_age_group,
    'Average Purchase Price': avg_price_purchange_by_age_group,
    'Total Purchase Value': Total_purchase_value_by_age_group,
    'Avg Total Purchase per Person':Avg_Total_Purchase_per_Person_by_age_group
})
# Format style
Purchasing_Analysis_Summary['Average Purchase Price'] = Purchasing_Analysis_Summary['Average Purchase Price'].astype(float).map("${:,.2f}".format)
Purchasing_Analysis_Summary['Total Purchase Value'] = Purchasing_Analysis_Summary['Total Purchase Value'].astype(float).map("${:,.2f}".format)
Purchasing_Analysis_Summary['Avg Total Purchase per Person'] = Purchasing_Analysis_Summary['Avg Total Purchase per Person'].astype(float).map("${:,.2f}".format)

```

<table id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630f" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Purchase Count</th> 
        <th class="col_heading level0 col1" >Average Purchase Price</th> 
        <th class="col_heading level0 col2" >Total Purchase Value</th> 
        <th class="col_heading level0 col3" >Average Purchase Total per Person</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630flevel0_row0" class="row_heading level0 row0" ><10</th> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow0_col0" class="data row0 col0" >23</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow0_col1" class="data row0 col1" >$3.35</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow0_col2" class="data row0 col2" >$77.13</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow0_col3" class="data row0 col3" >$4.54</td> 
    </tr>    <tr> 
        <th id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630flevel0_row1" class="row_heading level0 row1" >10-14</th> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow1_col0" class="data row1 col0" >28</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow1_col1" class="data row1 col1" >$2.96</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow1_col2" class="data row1 col2" >$82.78</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow1_col3" class="data row1 col3" >$3.76</td> 
    </tr>    <tr> 
        <th id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630flevel0_row2" class="row_heading level0 row2" >15-19</th> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow2_col0" class="data row2 col0" >136</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow2_col1" class="data row2 col1" >$3.04</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow2_col2" class="data row2 col2" >$412.89</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow2_col3" class="data row2 col3" >$3.86</td> 
    </tr>    <tr> 
        <th id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630flevel0_row3" class="row_heading level0 row3" >20-24</th> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow3_col0" class="data row3 col0" >365</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow3_col1" class="data row3 col1" >$3.05</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow3_col2" class="data row3 col2" >$1,114.06</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow3_col3" class="data row3 col3" >$4.32</td> 
    </tr>    <tr> 
        <th id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630flevel0_row4" class="row_heading level0 row4" >25-29</th> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow4_col0" class="data row4 col0" >101</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow4_col1" class="data row4 col1" >$2.90</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow4_col2" class="data row4 col2" >$293.00</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow4_col3" class="data row4 col3" >$3.81</td> 
    </tr>    <tr> 
        <th id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630flevel0_row5" class="row_heading level0 row5" >30-34</th> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow5_col0" class="data row5 col0" >73</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow5_col1" class="data row5 col1" >$2.93</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow5_col2" class="data row5 col2" >$214.00</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow5_col3" class="data row5 col3" >$4.12</td> 
    </tr>    <tr> 
        <th id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630flevel0_row6" class="row_heading level0 row6" >35-39</th> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow6_col0" class="data row6 col0" >41</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow6_col1" class="data row6 col1" >$3.60</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow6_col2" class="data row6 col2" >$147.67</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow6_col3" class="data row6 col3" >$4.76</td> 
    </tr>    <tr> 
        <th id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630flevel0_row7" class="row_heading level0 row7" >40+</th> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow7_col0" class="data row7 col0" >13</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow7_col1" class="data row7 col1" >$2.94</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow7_col2" class="data row7 col2" >$38.24</td> 
        <td id="T_8ecc59ba_9c53_11e8_8417_d49a20d1630frow7_col3" class="data row7 col3" >$3.19</td> 
    </tr></tbody> 
</table> 

 
 
 
 
### Top Spenders

* Identify the the top 5 spenders in the game by total purchase value, then list (in a table):
  * SN
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value
  
```python
# Group purchase data by screen names
spender_stats = purchase_data.groupby("SN")

# Count the total purchases by name
purchase_count_spender = spender_stats["Purchase ID"].count()

# Calculate the average purchase by name 
avg_purchase_price_spender = spender_stats["Price"].mean()

# Calculate purchase total 
purchase_total_spender = spender_stats["Price"].sum()

# Create data frame with obtained values
top_spenders = pd.DataFrame({"Purchase Count": purchase_count_spender,
                             "Average Purchase Price": avg_purchase_price_spender,
                             "Total Purchase Value":purchase_total_spender})

# Sort in descending order to obtain top 5 spender names 
formatted_spenders = top_spenders.sort_values(["Total Purchase Value"], ascending=False).head()

# Format with currency style
formatted_spenders.style.format({"Average Purchase Price":"${:,.2f}", 
                                 "Total Purchase Value":"${:,.2f}"})
```

<table id="T_8ecfe534_9c53_11e8_9489_d49a20d1630f" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Purchase Count</th> 
        <th class="col_heading level0 col1" >Average Purchase Price</th> 
        <th class="col_heading level0 col2" >Total Purchase Value</th> 
    </tr>    <tr> 
        <th class="index_name level0" >SN</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_8ecfe534_9c53_11e8_9489_d49a20d1630flevel0_row0" class="row_heading level0 row0" >Lisosia93</th> 
        <td id="T_8ecfe534_9c53_11e8_9489_d49a20d1630frow0_col0" class="data row0 col0" >5</td> 
        <td id="T_8ecfe534_9c53_11e8_9489_d49a20d1630frow0_col1" class="data row0 col1" >$3.79</td> 
        <td id="T_8ecfe534_9c53_11e8_9489_d49a20d1630frow0_col2" class="data row0 col2" >$18.96</td> 
    </tr>    <tr> 
        <th id="T_8ecfe534_9c53_11e8_9489_d49a20d1630flevel0_row1" class="row_heading level0 row1" >Idastidru52</th> 
        <td id="T_8ecfe534_9c53_11e8_9489_d49a20d1630frow1_col0" class="data row1 col0" >4</td> 
        <td id="T_8ecfe534_9c53_11e8_9489_d49a20d1630frow1_col1" class="data row1 col1" >$3.86</td> 
        <td id="T_8ecfe534_9c53_11e8_9489_d49a20d1630frow1_col2" class="data row1 col2" >$15.45</td> 
    </tr>    <tr> 
        <th id="T_8ecfe534_9c53_11e8_9489_d49a20d1630flevel0_row2" class="row_heading level0 row2" >Chamjask73</th> 
        <td id="T_8ecfe534_9c53_11e8_9489_d49a20d1630frow2_col0" class="data row2 col0" >3</td> 
        <td id="T_8ecfe534_9c53_11e8_9489_d49a20d1630frow2_col1" class="data row2 col1" >$4.61</td> 
        <td id="T_8ecfe534_9c53_11e8_9489_d49a20d1630frow2_col2" class="data row2 col2" >$13.83</td> 
    </tr>    <tr> 
        <th id="T_8ecfe534_9c53_11e8_9489_d49a20d1630flevel0_row3" class="row_heading level0 row3" >Iral74</th> 
        <td id="T_8ecfe534_9c53_11e8_9489_d49a20d1630frow3_col0" class="data row3 col0" >4</td> 
        <td id="T_8ecfe534_9c53_11e8_9489_d49a20d1630frow3_col1" class="data row3 col1" >$3.40</td> 
        <td id="T_8ecfe534_9c53_11e8_9489_d49a20d1630frow3_col2" class="data row3 col2" >$13.62</td> 
    </tr>    <tr> 
        <th id="T_8ecfe534_9c53_11e8_9489_d49a20d1630flevel0_row4" class="row_heading level0 row4" >Iskadarya95</th> 
        <td id="T_8ecfe534_9c53_11e8_9489_d49a20d1630frow4_col0" class="data row4 col0" >3</td> 
        <td id="T_8ecfe534_9c53_11e8_9489_d49a20d1630frow4_col1" class="data row4 col1" >$4.37</td> 
        <td id="T_8ecfe534_9c53_11e8_9489_d49a20d1630frow4_col2" class="data row4 col2" >$13.10</td> 
    </tr></tbody> 
</table> 


### Most Popular Items

* Identify the 5 most popular items by purchase count, then list (in a table):
  * Item ID
  * Item Name
  * Purchase Count
  * Item Price
  * Total Purchase Value
 
 ```python
 
 # create a df with above 3 cols
item_df = purchase_data[['Item ID','Item Name','Price']]

#group by Item ID & Item Name
item_stats = item_df.groupby(['Item ID','Item Name'])

# purchase count
Item_Purchase_Count = item_stats['Price'].count()

# Total Purchase count
Item_Total_Purchase_Value = (item_stats['Price'].sum())

# Average Item price
Item_average_item_price = (item_stats['Price'].mean())

# Create summary DF
item_summary = pd.DataFrame({"Purchase Count":Item_Purchase_Count,
                            "Item Price": Item_average_item_price,
                             "Total Purchase Value":Item_Total_Purchase_Value
                            })

item_summary_formatted =item_summary.sort_values(['Purchase Count'],ascending=False).head()

# Format with currency style
item_summary_formatted.style.format({"Item Price":"${:,.2f}",
                                "Total Purchase Value":"${:,.2f}"})
 
 ```
 
 <table id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630f" > 
<thead>    <tr> 
        <th class="blank" ></th> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Purchase Count</th> 
        <th class="col_heading level0 col1" >Item Price</th> 
        <th class="col_heading level0 col2" >Total Purchase Value</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Item ID</th> 
        <th class="index_name level1" >Item Name</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630flevel0_row0" class="row_heading level0 row0" >92</th> 
        <th id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630flevel1_row0" class="row_heading level1 row0" >Final Critic</th> 
        <td id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630frow0_col0" class="data row0 col0" >13</td> 
        <td id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630frow0_col1" class="data row0 col1" >$4.61</td> 
        <td id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630frow0_col2" class="data row0 col2" >$59.99</td> 
    </tr>    <tr> 
        <th id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630flevel0_row1" class="row_heading level0 row1" >178</th> 
        <th id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630flevel1_row1" class="row_heading level1 row1" >Oathbreaker, Last Hope of the Breaking Storm</th> 
        <td id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630frow1_col0" class="data row1 col0" >12</td> 
        <td id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630frow1_col1" class="data row1 col1" >$4.23</td> 
        <td id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630frow1_col2" class="data row1 col2" >$50.76</td> 
    </tr>    <tr> 
        <th id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630flevel0_row2" class="row_heading level0 row2" >145</th> 
        <th id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630flevel1_row2" class="row_heading level1 row2" >Fiery Glass Crusader</th> 
        <td id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630frow2_col0" class="data row2 col0" >9</td> 
        <td id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630frow2_col1" class="data row2 col1" >$4.58</td> 
        <td id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630frow2_col2" class="data row2 col2" >$41.22</td> 
    </tr>    <tr> 
        <th id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630flevel0_row3" class="row_heading level0 row3" >132</th> 
        <th id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630flevel1_row3" class="row_heading level1 row3" >Persuasion</th> 
        <td id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630frow3_col0" class="data row3 col0" >9</td> 
        <td id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630frow3_col1" class="data row3 col1" >$3.22</td> 
        <td id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630frow3_col2" class="data row3 col2" >$28.99</td> 
    </tr>    <tr> 
        <th id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630flevel0_row4" class="row_heading level0 row4" >108</th> 
        <th id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630flevel1_row4" class="row_heading level1 row4" >Extraction, Quickblade Of Trembling Hands</th> 
        <td id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630frow4_col0" class="data row4 col0" >9</td> 
        <td id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630frow4_col1" class="data row4 col1" >$3.53</td> 
        <td id="T_8ed36afe_9c53_11e8_8b74_d49a20d1630frow4_col2" class="data row4 col2" >$31.77</td> 
    </tr></tbody> 
</table> 


 
 

### Most Profitable Items

* Identify the 5 most profitable items by total purchase value, then list (in a table):
  * Item ID
  * Item Name
  * Purchase Count
  * Item Price
  * Total Purchase Value

```python

sorted_total_purchase =item_summary.sort_values(['Total Purchase Value'],ascending=False).head()
# Format with currency style
sorted_total_purchase.style.format({"Item Price":"${:,.2f}",
                                "Total Purchase Value":"${:,.2f}"})

```

<table id="T_8ed59b08_9c53_11e8_842e_d49a20d1630f" > 
<thead>    <tr> 
        <th class="blank" ></th> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Purchase Count</th> 
        <th class="col_heading level0 col1" >Item Price</th> 
        <th class="col_heading level0 col2" >Total Purchase Value</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Item ID</th> 
        <th class="index_name level1" >Item Name</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_8ed59b08_9c53_11e8_842e_d49a20d1630flevel0_row3" class="row_heading level0 row3" >92</th> 
        <th id="T_8ed59b08_9c53_11e8_842e_d49a20d1630flevel1_row3" class="row_heading level1 row3" >Final Critic</th> 
        <td id="T_8ed59b08_9c53_11e8_842e_d49a20d1630frow3_col0" class="data row3 col0" >13</td> 
        <td id="T_8ed59b08_9c53_11e8_842e_d49a20d1630frow3_col1" class="data row3 col1" >$4.61</td> 
        <td id="T_8ed59b08_9c53_11e8_842e_d49a20d1630frow3_col2" class="data row3 col2" >$59.99</td> 
    </tr>  <tr> 
        <th id="T_8ed59b08_9c53_11e8_842e_d49a20d1630flevel0_row0" class="row_heading level0 row0" >178</th> 
        <th id="T_8ed59b08_9c53_11e8_842e_d49a20d1630flevel1_row0" class="row_heading level1 row0" >Oathbreaker, Last Hope of the Breaking Storm</th> 
        <td id="T_8ed59b08_9c53_11e8_842e_d49a20d1630frow0_col0" class="data row0 col0" >12</td> 
        <td id="T_8ed59b08_9c53_11e8_842e_d49a20d1630frow0_col1" class="data row0 col1" >$4.23</td> 
        <td id="T_8ed59b08_9c53_11e8_842e_d49a20d1630frow0_col2" class="data row0 col2" >$50.76</td> 
    </tr>    <tr> 
        <th id="T_8ed59b08_9c53_11e8_842e_d49a20d1630flevel0_row1" class="row_heading level0 row1" >82</th> 
        <th id="T_8ed59b08_9c53_11e8_842e_d49a20d1630flevel1_row1" class="row_heading level1 row1" >Nirvana</th> 
        <td id="T_8ed59b08_9c53_11e8_842e_d49a20d1630frow1_col0" class="data row1 col0" >9</td> 
        <td id="T_8ed59b08_9c53_11e8_842e_d49a20d1630frow1_col1" class="data row1 col1" >$4.90</td> 
        <td id="T_8ed59b08_9c53_11e8_842e_d49a20d1630frow1_col2" class="data row1 col2" >$44.10</td> 
    </tr>    <tr> 
        <th id="T_8ed59b08_9c53_11e8_842e_d49a20d1630flevel0_row2" class="row_heading level0 row2" >145</th> 
        <th id="T_8ed59b08_9c53_11e8_842e_d49a20d1630flevel1_row2" class="row_heading level1 row2" >Fiery Glass Crusader</th> 
        <td id="T_8ed59b08_9c53_11e8_842e_d49a20d1630frow2_col0" class="data row2 col0" >9</td> 
        <td id="T_8ed59b08_9c53_11e8_842e_d49a20d1630frow2_col1" class="data row2 col1" >$4.58</td> 
        <td id="T_8ed59b08_9c53_11e8_842e_d49a20d1630frow2_col2" class="data row2 col2" >$41.22</td> 
    </tr>   <tr> 
        <th id="T_8ed59b08_9c53_11e8_842e_d49a20d1630flevel0_row4" class="row_heading level0 row4" >103</th> 
        <th id="T_8ed59b08_9c53_11e8_842e_d49a20d1630flevel1_row4" class="row_heading level1 row4" >Singed Scalpel</th> 
        <td id="T_8ed59b08_9c53_11e8_842e_d49a20d1630frow4_col0" class="data row4 col0" >8</td> 
        <td id="T_8ed59b08_9c53_11e8_842e_d49a20d1630frow4_col1" class="data row4 col1" >$4.35</td> 
        <td id="T_8ed59b08_9c53_11e8_842e_d49a20d1630frow4_col2" class="data row4 col2" >$34.80</td> 
    </tr></tbody> 
</table> 





As final considerations:

* You must use the Pandas Library and the Jupyter Notebook.
* You must submit a link to your Jupyter Notebook with the viewable Data Frames.
* You must include a written description of three observable trends based on the data.
* See [Example Solution](HeroesOfPymoli/HeroesOfPymoli_starter.ipynb) for a reference on expected format.

## Option 2: PyCitySchools

![Education](Images/education.png)

Well done! Having spent years analyzing financial records for big banks, you've finally scratched your idealistic itch and joined the education sector. In your latest role, you've become the Chief Data Scientist for your city's school district. In this capacity, you'll be helping the  school board and mayor make strategic decisions regarding future school budgets and priorities.

As a first task, you've been asked to analyze the district-wide standardized test results. You'll be given access to every student's math and reading scores, as well as various information on the schools they attend. Your responsibility is to aggregate the data to and showcase obvious trends in school performance.

Your final report should include each of the following:

### District Summary

```
# Dependencies and Setup
import pandas as pd

# File to Load (Remember to Change These)
school_data_to_load = "Resources/schools_complete.csv"
student_data_to_load = "Resources/students_complete.csv"

# Read School and Student Data File and store into Pandas DataFrames
school_data = pd.read_csv(school_data_to_load)
student_data = pd.read_csv(student_data_to_load)

# Combine the data into a single dataset.  
school_data_complete = pd.merge(student_data, school_data, how="left", on=["school_name", "school_name"])
```
* Create a high level snapshot (in table form) of the district's key metrics, including:
  * Total Schools
  * Total Students
  * Total Budget
  * Average Math Score
  * Average Reading Score
  * % Passing Math (The percentage of students that passed math.)
  * % Passing Reading (The percentage of students that passed reading.)
  * % Overall Passing (The percentage of students that passed math **and** reading.)
```
# Calculate the total number of schools
total_schools = len(school_data['school_name'].unique())

# Calculate the total number of students
total_students = len(student_data['student_name'])

#Calculate Total Budget
total_budget = school_data_complete['budget'].unique().sum()

#Calculate average math score
avg_math_score = school_data_complete['math_score'].mean()

# Calculate average reading score
avg_reading_score = school_data_complete['reading_score'].mean()

# Calculate the percentage of students with a passing math score (70 or greater)
students_math_with_above_70 = student_data.loc[(student_data['math_score']) >= 70].count()
percentage_students_math_with_above_70=students_math_with_above_70['math_score']/total_students * 100

# Calculate the percentage of students with a passing reading score (70 or greater)
students_reading_with_above_70 = school_data_complete.loc[(school_data_complete['reading_score']) >= 70].count()
percentage_students_reading_with_above_70 = students_reading_with_above_70['reading_score']/total_students * 100

# Calculate the percentage of students who passed math and reading (% Overall Passing)
total_pass_percentage = school_data_complete.loc[(school_data_complete['math_score'] >= 70) &
                                                (school_data_complete['reading_score'] >= 70)
                                                ].count()

overall_pass_percentage = total_pass_percentage['Student ID']/total_students * 100

district_sumary = pd.DataFrame([{
    "Total Schools": total_schools,
    "Total Students": total_students,
    "Total Budget": total_budget,
    "Average Math Score": avg_math_score,
    "Average Reading Score": avg_reading_score,
    "% Passing Math": percentage_students_math_with_above_70,
    "% Passing Reading": percentage_students_reading_with_above_70,
    "% Overall Passing": overall_pass_percentage
}])

# formatting total students and total budget columns
district_sumary['Total Students'] = district_sumary['Total Students'].astype(int).map("{:,}".format)
district_sumary['Total Budget'] = district_sumary['Total Budget'].astype(float).map("${:,.2f}".format)
district_sumary
```
<table id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630f" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Total Schools</th> 
        <th class="col_heading level0 col1" >Total Students</th> 
        <th class="col_heading level0 col2" >Total Budget</th> 
        <th class="col_heading level0 col3" >Average Math Score</th> 
        <th class="col_heading level0 col4" >Average Reading Score</th> 
        <th class="col_heading level0 col5" >% Passing Math</th> 
        <th class="col_heading level0 col6" >% Passing Reading</th> 
        <th class="col_heading level0 col7" >% Overall Passing</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row0" >0</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >15</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >39,170</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$24,649,428.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >78.985371</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >81.87784</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >74.980853</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >85.805463</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >65.172326</td> 
    </tr></tbody> 
</table> 


### School Summary

* Create an overview table that summarizes key metrics about each school, including:
  * School Name
  * School Type
  * Total Students
  * Total School Budget
  * Per Student Budget
  * Average Math Score
  * Average Reading Score
  * % Passing Math (The percentage of students that passed math.)
  * % Passing Reading (The percentage of students that passed reading.)
  * % Overall Passing (The percentage of students that passed math **and** reading.)

```
# create data series with only type value
grouped_school=school_data_complete.groupby(['school_name'])

# Total Students
total_students_by_school = school_data_complete.groupby('school_name')['student_name'].count()

# Total School Budget
total_budget_by_school = school_data.groupby(['school_name'])['budget'].sum()

# Per Student Budget
Per_Student_Budget=total_budget_by_school/total_students_by_school

#Average Math Score
average_math_score_by_school = student_data[['school_name','math_score']].groupby('school_name').mean()

#Average Reading Score
average_reading_score_by_school = student_data[['school_name','reading_score']].groupby('school_name').mean()

# % Passing Math
student_math_score_by_school = student_data.loc[(student_data['math_score']) >= 70].groupby('school_name').count()
Average_Math_Percentage_Score_by_school = student_math_score_by_school['math_score']/total_students_by_school * 100

# % Passing Reading
student_reading_score_by_school = student_data.loc[(student_data['reading_score']) >= 70].groupby('school_name').count()
Average_Reading_Percentage_Score_by_school = student_reading_score_by_school['reading_score']/total_students_by_school * 100

# % Overall Passing (The percentage of students that passed math and reading.)
total_pass_percentage_by_school = student_data.loc[(student_data['math_score'] >= 70) &
                                                (student_data['reading_score'] >= 70)
                                                ].groupby('school_name').count()

overall_pass_percentage_by_school = total_pass_percentage_by_school['Student ID']/total_students_by_school * 100

# create a summary data frame

school_summary = pd.DataFrame({'School Type': grouped_school['type'].first(),
                               'Total Students': total_students_by_school,
                               "Total School Budget":total_budget_by_school,
                              'Per Student Budget': Per_Student_Budget,
                              'Average Math Score': average_math_score_by_school['math_score'],
                               'Average Reading Score': average_reading_score_by_school['reading_score'],
                               '% Passing Math': Average_Math_Percentage_Score_by_school,
                               '% Passing Reading': Average_Reading_Percentage_Score_by_school,
                               '% Overall Passing': overall_pass_percentage_by_school
                              })
#formatting
school_summary['Total School Budget']=school_summary['Total School Budget'].astype(float).map("${:,.2f}".format)
school_summary['Per Student Budget']=school_summary['Per Student Budget'].astype(float).map("${:,.2f}".format)
school_summary
```

### Top Performing Schools (By % Overall Passing)

* Create a table that highlights the top 5 performing schools based on % Overall Passing. Include:
  * School Name
  * School Type
  * Total Students
  * Total School Budget
  * Per Student Budget
  * Average Math Score
  * Average Reading Score
  * % Passing Math (The percentage of students that passed math.)
  * % Passing Reading (The percentage of students that passed reading.)
  * % Overall Passing (The percentage of students that passed math **and** reading.)

```
school_summary.sort_values('% Overall Passing',ascending=False).head()

```

### Bottom Performing Schools (By % Overall Passing)

* Create a table that highlights the bottom 5 performing schools based on % Overall Passing. Include all of the same metrics as above.

```
school_summary.sort_values('% Overall Passing',ascending=True).head()

```

### Math Scores by Grade\*\*

* Create a table that lists the average Math Score for students of each grade level (9th, 10th, 11th, 12th) at each school.

```
avg_math_score_by_9th_grade = school_data_complete.loc[school_data_complete['grade']=='9th'].groupby('school_name')['math_score'].mean()
avg_math_score_by_10th_grade = school_data_complete.loc[school_data_complete['grade']=='10th'].groupby('school_name')['math_score'].mean()
avg_math_score_by_11th_grade = school_data_complete.loc[school_data_complete['grade']=='11th'].groupby('school_name')['math_score'].mean()
avg_math_score_by_12th_grade = school_data_complete.loc[school_data_complete['grade']=='12th'].groupby('school_name')['math_score'].mean()

Mathscores_summary = pd.DataFrame({
    '9th': avg_math_score_by_9th_grade,
    '10th': avg_math_score_by_10th_grade,
    '11th': avg_math_score_by_11th_grade,
    '12th': avg_math_score_by_12th_grade
})


```
### Reading Scores by Grade

* Create a table that lists the average Reading Score for students of each grade level (9th, 10th, 11th, 12th) at each school.
```

avg_reading_score_by_9th_grade = school_data_complete.loc[school_data_complete['grade']=='9th'].groupby('school_name')['reading_score'].mean()
avg_reading_score_by_10th_grade = school_data_complete.loc[school_data_complete['grade']=='10th'].groupby('school_name')['reading_score'].mean()
avg_reading_score_by_11th_grade = school_data_complete.loc[school_data_complete['grade']=='11th'].groupby('school_name')['reading_score'].mean()
avg_reading_score_by_12th_grade = school_data_complete.loc[school_data_complete['grade']=='12th'].groupby('school_name')['reading_score'].mean()

Reading_scores_summary = pd.DataFrame({
    '9th': avg_reading_score_by_9th_grade,
    '10th': avg_reading_score_by_10th_grade,
    '11th': avg_reading_score_by_11th_grade,
    '12th': avg_reading_score_by_12th_grade
})

```
### Scores by School Spending

* Create a table that breaks down school performances based on average Spending Ranges (Per Student). Use 4 reasonable bins to group school spending. Include in the table each of the following:
  * Average Math Score
  * Average Reading Score
  * % Passing Math (The percentage of students that passed math.)
  * % Passing Reading (The percentage of students that passed reading.)
  * % Overall Passing (The percentage of students that passed math **and** reading.)

### Scores by School Size

* Repeat the above breakdown, but this time group schools based on a reasonable approximation of school size (Small, Medium, Large).

### Scores by School Type

* Repeat the above breakdown, but this time group schools based on school type (Charter vs. District).

As final considerations:

* Use the pandas library and Jupyter Notebook.
* You must submit a link to your Jupyter Notebook with the viewable Data Frames.
* You must include a written description of at least two observable trends based on the data.
* See [Example Solution](PyCitySchools/PyCitySchools_starter.ipynb) for a reference on the expected format.

## Hints and Considerations

* These are challenging activities for a number of reasons. For one, these activities will require you to analyze thousands of records. Hacking through the data to look for obvious trends in Excel is just not a feasible option. The size of the data may seem daunting, but pandas will allow you to efficiently parse through it.

* Second, these activities will also challenge you by requiring you to learn on your feet. Don't fool yourself into thinking: "I need to study pandas more closely before diving in." Get the basic gist of the library and then _immediately_ get to work. When facing a daunting task, it's easy to think: "I'm just not ready to tackle it yet." But that's the surest way to never succeed. Learning to program requires one to constantly tinker, experiment, and learn on the fly. You are doing exactly the _right_ thing, if you find yourself constantly practicing Google-Fu and diving into documentation. There is just no way (or reason) to try and memorize it all. Online references are available for you to use when you need them. So use them!

* Take each of these tasks one at a time. Begin your work, answering the basic questions: "How do I import the data?" "How do I convert the data into a DataFrame?" "How do I build the first table?" Don't get intimidated by the number of asks. Many of them are repetitive in nature with just a few tweaks. Be persistent and creative!

* Expect these exercises to take time! Don't get discouraged if you find yourself spending  hours initially with little progress. Force yourself to deal with the discomfort of not knowing and forge ahead. Consider these hours an investment in your future!

* As always, feel encouraged to work in groups and get help from your TAs and Instructor. Just remember, true success comes from mastery and _not_ a completed homework assignment. So challenge yourself to truly succeed!

* Ensure your repository has regular commits (i.e. 20+ commits) and a thorough README.md file

### Copyright

Trilogy Education Services © 2019. All Rights Reserved.
