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

 # Format total students and total budget columns

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

<table id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630f" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >School Type</th> 
        <th class="col_heading level0 col1" >Total Students</th> 
        <th class="col_heading level0 col2" >Total School Budget</th> 
        <th class="col_heading level0 col3" >Per Stundent Budget</th>
        <th class="col_heading level0 col4" >Average Math Score</th> 
        <th class="col_heading level0 col5" >Average Reading Score</th> 
        <th class="col_heading level0 col6" >% Passing Math</th> 
        <th class="col_heading level0 col7" >% Passing Reading</th> 
        <th class="col_heading level0 col8" >% Overall Passing</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row0" >Bailey High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >District</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >4976</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$3,124,928.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$628.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >77.048432</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >81.033963</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >66.680064</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >81.933280</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >54.642283</td>
    </tr>
        <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row1" >Cabrera High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >Charter</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >1858</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$1,081,356.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$582.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >83.061895</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >83.975780</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >94.133477</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >97.039828</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >91.334769</td>
    </tr>
    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row2" >Figueroa High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >District</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >2949</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$1,884,411.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$639.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >76.711767</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >81.158020</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >65.988471</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >80.739234</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >53.204476</td>
    </tr>
    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row3" >Ford High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >District</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >2739</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$1,763,916.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$644.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >77.102592</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >80.746258</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >68.309602</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >79.299014</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >54.289887</td>
    </tr>
    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row4" >Griffin High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >Charter</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >1468</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$917,500.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$625.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >83.351499</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >83.816757</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >93.392371</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >97.138965</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >90.599455</td>
    </tr>
    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Hernandez High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >District</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >4635</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$3,022,020.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$652.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >77.289752</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >80.934412</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >66.752967</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >80.862999</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >53.527508</td>
    </tr>
    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row6" >Holden High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >Charter</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >427</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$248,087.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$581.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >83.803279</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >83.814988</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >92.505855</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >96.252927</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >89.227166</td>
    </tr>
    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row7" >Huang High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >District</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >2917</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$1,910,635.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$655.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >76.629414</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >81.182722</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >65.683922</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >81.316421</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >53.513884</td>
    </tr>
    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row8" >Johnson High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >District</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >4761</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$3,094,650.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$650.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >77.072464</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >80.966394</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >66.057551</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >81.222432</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >53.539172</td>
    </tr>
     <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row9" >Pena High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >Charter</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >962</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$585,858.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$609.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >83.839917</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >84.044699</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >94.594595</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >95.945946</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >90.540541</td>
    </tr>
    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row10" >Rodriguez High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >District</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >3999</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$2,547,363.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$637.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >76.842711</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >80.744686</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >66.366592</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >80.220055</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >52.988247</td>
    </tr>
    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row11" >Shelton High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >Charter</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >1761</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$1,056,600.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$600.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >83.359455</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >83.725724</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >93.867121</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >95.854628</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >89.892107</td>
    </tr>
    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row12" >Thomas High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >Charter</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >1635</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$1,043,130.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$638.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >83.418349</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >83.848930</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >93.272171</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >97.308869</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >90.582567</td>
    </tr>
    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row13" >Wilson High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >Charter</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >2283</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$1,319,574.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$578.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >83.274201</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >83.989488</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >93.867718</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >96.539641</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >90.582567</td>
    </tr>
    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row14" >Wright High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >Charter</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >1800</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$1,049,400.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$583.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >83.682222</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >83.955000</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >93.333333</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >96.611111</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >90.333333</td>
    </tr></tbody> 
</table> 



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

<table id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630f" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >School Type</th> 
        <th class="col_heading level0 col1" >Total Students</th> 
        <th class="col_heading level0 col2" >Total School Budget</th> 
        <th class="col_heading level0 col3" >Per Stundent Budget</th>
        <th class="col_heading level0 col4" >Average Math Score</th> 
        <th class="col_heading level0 col5" >Average Reading Score</th> 
        <th class="col_heading level0 col6" >% Passing Math</th> 
        <th class="col_heading level0 col7" >% Passing Reading</th> 
        <th class="col_heading level0 col8" >% Overall Passing</th> 
    </tr></thead> 
<tbody>    
        <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row1" >Cabrera High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >Charter</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >1858</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$1,081,356.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$582.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >83.061895</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >83.975780</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >94.133477</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >97.039828</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >91.334769</td>
    </tr>
     <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row12" >Thomas High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >Charter</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >1635</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$1,043,130.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$638.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >83.418349</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >83.848930</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >93.272171</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >97.308869</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >90.582567</td>
    </tr>
    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row4" >Griffin High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >Charter</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >1468</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$917,500.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$625.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >83.351499</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >83.816757</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >93.392371</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >97.138965</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >90.599455</td>
    </tr>
    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row13" >Wilson High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >Charter</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >2283</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$1,319,574.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$578.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >83.274201</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >83.989488</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >93.867718</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >96.539641</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >90.582567</td>
    </tr>
    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row9" >Pena High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >Charter</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >962</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$585,858.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$609.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >83.839917</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >84.044699</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >94.594595</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >95.945946</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >90.540541</td>
    </tr></tbody> 
</table> 

### Bottom Performing Schools (By % Overall Passing)

* Create a table that highlights the bottom 5 performing schools based on % Overall Passing. Include all of the same metrics as above.

```
school_summary.sort_values('% Overall Passing',ascending=True).head()

```

<table id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630f" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >School Type</th> 
        <th class="col_heading level0 col1" >Total Students</th> 
        <th class="col_heading level0 col2" >Total School Budget</th> 
        <th class="col_heading level0 col3" >Per Stundent Budget</th>
        <th class="col_heading level0 col4" >Average Math Score</th> 
        <th class="col_heading level0 col5" >Average Reading Score</th> 
        <th class="col_heading level0 col6" >% Passing Math</th> 
        <th class="col_heading level0 col7" >% Passing Reading</th> 
        <th class="col_heading level0 col8" >% Overall Passing</th> 
    </tr></thead> 
<tbody> 
    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row10" >Rodriguez High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >District</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >3999</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$2,547,363.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$637.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >76.842711</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >80.744686</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >66.366592</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >80.220055</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >52.988247</td>
    </tr>        
    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row2" >Figueroa High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >District</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >2949</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$1,884,411.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$639.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >76.711767</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >81.158020</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >65.988471</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >80.739234</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >53.204476</td>
    </tr>
     <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row7" >Huang High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >District</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >2917</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$1,910,635.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$655.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >76.629414</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >81.182722</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >65.683922</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >81.316421</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >53.513884</td>
    </tr>
    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Hernandez High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >District</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >4635</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$3,022,020.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$652.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >77.289752</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >80.934412</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >66.752967</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >80.862999</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >53.527508</td>
    </tr>
    <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row8" >Johnson High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >District</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >4761</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >$3,094,650.00</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >$650.0</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col4" >77.072464</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col5" >80.966394</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col6" >66.057551</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col7" >81.222432</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col8" >53.539172</td>
    </tr></tbody> 
</table> 





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

<table id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630f" > 
<thead><tr> 
        <th class="blank level0" >school_name</th>  
        <th class="col_heading level0 col0" >9th</th> 
        <th class="col_heading level0 col1" >10th</th> 
        <th class="col_heading level0 col2" >11th</th>
        <th class="col_heading level0 col3" >12th</th> 
    </tr></thead> 
<tbody> <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row0" >Bailey High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >77.083676</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >76.996772</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >77.515588</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >76.492218</td> 
    </tr><tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row1" >Cabrera High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >83.094697</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >83.154506</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >82.765560</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >83.277487</td> 
     </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row2" >Figueroa High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >76.403037</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >76.539974</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >76.884344</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >77.151369</td> 
      </tr> <tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row3" >Ford High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >77.361345</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >77.672316</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >76.918058</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >76.179963</td> 
      </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row4" >Griffin High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >82.044010</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >84.229064</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >83.842105</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >83.356164</td> 
      </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Hernandez High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >77.438495</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >77.337408</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >77.136029</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >77.186567</td> 
       </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Holden High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >83.787402</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >83.429825</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >85.000000</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >82.855422</td> 
       </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Huang High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >77.027251</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >75.908735</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >76.446602</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >77.225641</td> 
       </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Johnson High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >77.187857</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >76.691117</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >77.491653</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >76.863248</td> 
       </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Pena High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >83.625455</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >83.372000</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >84.328125</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >84.121547</td> 
       </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Rodriguez High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >76.859966</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >76.612500</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >76.395626</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >77.690748</td> 
       </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Shelton High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >83.420755</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >82.917411</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >83.383495</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >83.778976</td> 
       </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Thomas High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >83.590022</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >83.087886</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >83.498795</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >83.497041</td> 
       </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Wilson High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >83.085578</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >83.724422</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >83.195326</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >83.035794</td> 
       </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Wright High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >83.264706</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >84.010288</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >83.836782</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >83.644986</td> 
       </tr></tbody>
 </table> 

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

<table id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630f" > 
<thead><tr> 
        <th class="blank level0" >school_name</th>  
        <th class="col_heading level0 col0" >9th</th> 
        <th class="col_heading level0 col1" >10th</th> 
        <th class="col_heading level0 col2" >11th</th>
        <th class="col_heading level0 col3" >12th</th> 
    </tr></thead> 
<tbody> <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row0" >Bailey High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >81.303155</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >80.907183</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >80.945643</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >80.912451</td> 
    </tr><tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row1" >Cabrera High School</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >83.676136</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >84.253219</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >83.788382</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >84.287958</td> 
     </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row2" >Figueroa High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >81.198598</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >81.408912</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >80.640339</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >81.384863</td> 
      </tr> <tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row3" >Ford High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >80.632653</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >81.262712</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >80.403642</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >80.662338</td> 
      </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row4" >Griffin High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >83.369193</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >83.706897</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >84.288089</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >84.013699</td> 
      </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Hernandez High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >80.866860</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >80.660147</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >81.396140</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >80.857143</td> 
       </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Holden High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >83.677165</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >83.324561</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >83.815534</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >84.698795</td> 
       </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Huang High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >81.290284</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >81.512386</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >81.417476</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >80.305983</td> 
       </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Johnson High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >81.260714</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >80.773431</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >80.616027</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >81.227564</td> 
       </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Pena High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >83.807273</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >83.612000</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >84.335938</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >84.591160</td> 
       </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Rodriguez High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >80.993127</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >80.629808</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >80.864811</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >80.376426</td> 
       </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Shelton High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >84.122642</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >83.441964</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >84.373786</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >82.781671</td> 
       </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Thomas High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >83.728850</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >84.254157</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >83.585542</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >83.831361</td> 
       </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Wilson High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >83.939778</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >84.021452</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >83.764608</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >84.317673</td> 
       </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row5" >Wright High School</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >83.833333</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >83.812757</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >84.156322</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >84.073171</td> 
       </tr></tbody>
 </table> 


### Scores by School Spending

* Create a table that breaks down school performances based on average Spending Ranges (Per Student). Use 4 reasonable bins to group school spending. Include in the table each of the following:
  * Average Math Score
  * Average Reading Score
  * % Passing Math (The percentage of students that passed math.)
  * % Passing Reading (The percentage of students that passed reading.)
  * % Overall Passing (The percentage of students that passed math **and** reading.)
  
```
bins = [0,583.99,629.99,644.99,674]
group_names=['<$584',"$585-629",'$630-644','$645-$675']

Avg_Spending = school_summary.loc[:,['Average Math Score','Average Reading Score','% Passing Math','% Passing Reading','% Overall Passing']]

Avg_Spending['Spending Ranges (Per Student)'] = pd.cut(school_summary['Per Student Budget'],bins,labels=group_names,include_lowest=True) 

Avg_Spending = Avg_Spending.groupby('Spending Ranges (Per Student)').mean()

Avg_Spending.style.format({
    'Average Math Score':"{:,.2f}",
    'Average Reading Score':"{:,.2f}",
    '% Passing Math':"{:,.2f}",'% Passing Reading':"{:,.2f}",
    '% Overall Passing':"{:,.2f}"})

```

<table id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630f" > 
<thead><tr> 
        <th class="blank level1" >Spending Ranges (Per Student)</th>  
        <th class="col_heading level0 col0" >Average Math Score	</th> 
        <th class="col_heading level0 col1" >Average Reading Score	</th> 
        <th class="col_heading level0 col2" >% Passing Math</th>
        <th class="col_heading level0 col3" >% Passing Reading</th>
        <th class="col_heading level0 col4" >% Overall Passing</th>
    </tr></thead> 
<tbody> <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row0" ><$584</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >83.46</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >83.93</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >93.46</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >96.61</td>
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >90.37</td> 
    </tr><tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row1" >585-629</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >81.90</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >83.16</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >87.13</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >92.72</td>
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >81.42</td>
     </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row2" >630-644</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >78.52</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >81.62</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >73.48</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >84.39</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >62.86</td>
      </tr> <tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row3" >645-675</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >77.00</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >81.03</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >66.16</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >81.13</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >53.53</td> 
      </tr><tr> 
</table>

### Scores by School Size

* Repeat the above breakdown, but this time group schools based on a reasonable approximation of school size (Small, Medium, Large).

```
bins = [0,999.99,1999.99,9999]
group_names=['Small (<1000)',"Medium (1000-2000)",'Large (2000-5000)']

School_size = school_summary.loc[:,['Average Math Score','Average Reading Score','% Passing Math','% Passing Reading','% Overall Passing']]

School_size['School Size'] = pd.cut(school_summary['Total Students'],bins,labels=group_names,include_lowest=True) 

School_size = School_size.groupby('School Size').mean()

School_size

```

<table id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630f" > 
<thead><tr> 
        <th class="blank level1" >School Size</th>  
        <th class="col_heading level0 col0" >Average Math Score	</th> 
        <th class="col_heading level0 col1" >Average Reading Score	</th> 
        <th class="col_heading level0 col2" >% Passing Math</th>
        <th class="col_heading level0 col3" >% Passing Reading</th>
        <th class="col_heading level0 col4" >% Overall Passing</th>
    </tr></thead> 
<tbody> <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row0" >Small(<1000)</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >83.821598</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >83.929843</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >93.550225</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >96.099437</td>
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >89.883853</td> 
    </tr><tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row1" >Medium(1000-2000)</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >83.374684</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >83.864438</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >93.599695</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >96.790680</td>
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >90.621535</td>
     </tr><tr> 
          <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row2" >Large(2000-5000)</th> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >77.746417</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >81.344493</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >69.963361</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >82.766634</td> 
          <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >58.286003</td>
      </tr><tr> 
</table>




### Scores by School Type

* Repeat the above breakdown, but this time group schools based on school type (Charter vs. District).

```

School_Type = school_summary.loc[:,['School Type','Average Math Score','Average Reading Score','% Passing Math','% Passing Reading','% Overall Passing']]
School_Type = School_Type.groupby('School Type').mean()
School_Type

```

<table id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630f" > 
<thead><tr> 
        <th class="blank level1" >School Type</th>  
        <th class="col_heading level0 col0" >Average Math Score	</th> 
        <th class="col_heading level0 col1" >Average Reading Score	</th> 
        <th class="col_heading level0 col2" >% Passing Math</th>
        <th class="col_heading level0 col3" >% Passing Reading</th>
        <th class="col_heading level0 col4" >% Overall Passing</th>
    </tr></thead> 
<tbody> <tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row0" >Charter</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >83.473852</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >83.896421</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >93.620830</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >96.586489</td>
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >90.432244</td> 
    </tr><tr> 
        <th id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630flevel0_row0" class="row_heading level0 row1" >District</th> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col0" class="data row0 col0" >76.956733</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col1" class="data row0 col1" >80.966636</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col2" class="data row0 col2" >66.548453</td> 
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >80.799062</td>
        <td id="T_8eab2a8a_9c53_11e8_bca9_d49a20d1630frow0_col3" class="data row0 col3" >53.672208</td>
     </tr><tr> 
</table>

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
