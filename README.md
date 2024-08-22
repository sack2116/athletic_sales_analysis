## Athletics Sales Analysis

### Overview

This project involves analyzing sales data to gain insights into the athletic wear market across the U.S. over two years. The analysis will cover various aspects, including total sales by region, top retailers, and sales trends for women's athletic footwear
You will analyze sales data to:

** Determine which cities have sold the most athletic wear.
** Identify retailers with the greatest total sales and those that sold the most women’s athletic footwear.
** Find out which day and week had the highest sales for women’s athletic footwear.

Functions and Methods
1. Combine and Clean the Data
Arguments:

athletic_sales_2020.csv (str): Path to the 2020 sales data CSV file.
athletic_sales_2021.csv (str): Path to the 2021 sales data CSV file.
Returns:

combined_df (DataFrame): A DataFrame combining the 2020 and 2021 sales data with cleaned columns.
Examples:

python
Copy code
# Importing libraries
import pandas as pd

# Loading data
df_2020 = pd.read_csv('athletic_sales_2020.csv')
df_2021 = pd.read_csv('athletic_sales_2021.csv')

# Combining data
combined_df = pd.concat([df_2020, df_2021], ignore_index=True)

# Cleaning data
combined_df['invoice_date'] = pd.to_datetime(combined_df['invoice_date'])
combined_df.dropna(inplace=True)
Pseudocode:

Load the CSV files into DataFrames.
Combine DataFrames using concatenation.
Convert the invoice_date column to datetime.
Check and handle missing values.
Reset the index of the combined DataFrame.
2. Determine Which Region Sold the Most Products
Arguments:

combined_df (DataFrame): The DataFrame containing the combined sales data.
Returns:

region_sales (DataFrame): A DataFrame showing the top five regions with the most products sold.
Examples:

python
Copy code
# Aggregating data
region_sales = combined_df.groupby(['region', 'state', 'city']).size().reset_index(name='total_products')

# Sorting results
region_sales_sorted = region_sales.sort_values(by='total_products', ascending=False).head(5)
Pseudocode:

Group the DataFrame by region, state, and city.
Count the number of products sold in each group.
Sort the results in descending order.
Select the top five regions.
3. Determine Which Region Had the Most Sales
Arguments:

combined_df (DataFrame): The DataFrame containing the combined sales data.
Returns:

region_sales_amount (DataFrame): A DataFrame showing the top five regions with the highest sales.
Examples:

python
Copy code
# Aggregating data
region_sales_amount = combined_df.groupby(['region', 'state', 'city'])['total_sales'].sum().reset_index(name='total_sales')

# Sorting results
region_sales_amount_sorted = region_sales_amount.sort_values(by='total_sales', ascending=False).head(5)
Pseudocode:

Group the DataFrame by region, state, and city.
Sum the total sales in each group.
Sort the results in descending order.
Select the top five regions by total sales.
4. Determine Which Retailer Had the Most Sales
Arguments:

combined_df (DataFrame): The DataFrame containing the combined sales data.
Returns:

retailer_sales (DataFrame): A DataFrame showing the top five retailers with the highest sales.
Examples:

python
Copy code
# Aggregating data
retailer_sales = combined_df.groupby(['retailer', 'region', 'state', 'city'])['total_sales'].sum().reset_index(name='total_sales')

# Sorting results
retailer_sales_sorted = retailer_sales.sort_values(by='total_sales', ascending=False).head(5)
Pseudocode:

Group the DataFrame by retailer, region, state, and city.
Sum the total sales for each retailer.
Sort the results in descending order.
Select the top five retailers.
5. Determine Which Retailer Sold the Most Women’s Athletic Footwear
Arguments:

combined_df (DataFrame): The DataFrame containing the combined sales data.
Returns:

women_footwear_sales (DataFrame): A DataFrame showing the top five retailers that sold the most women’s athletic footwear.
Examples:

python
Copy code
# Filtering data
women_footwear_df = combined_df[combined_df['product_category'].str.contains('Women\'s Athletic Footwear')]

# Aggregating data
women_footwear_sales = women_footwear_df.groupby(['retailer', 'region', 'state', 'city']).size().reset_index(name='total_footwear_sales')

# Sorting results
women_footwear_sales_sorted = women_footwear_sales.sort_values(by='total_footwear_sales', ascending=False).head(5)
Pseudocode:

Filter the DataFrame to include only women’s athletic footwear.
Group by retailer, region, state, and city.
Count the number of sales in each group.
Sort the results in descending order.
Select the top five retailers.
6. Determine the Day with the Most Women’s Athletic Footwear Sales
Arguments:

women_footwear_df (DataFrame): Filtered DataFrame with only women’s athletic footwear data.
Returns:

daily_sales (DataFrame): A DataFrame showing the top 10 days with the highest sales for women’s athletic footwear.
Examples:

python
Copy code
# Pivot table for daily sales
daily_sales_pivot = women_footwear_df.pivot_table(index='invoice_date', values='total_sales', aggfunc='sum')

# Resampling and sorting
daily_sales_resampled = daily_sales_pivot.resample('D').sum()
daily_sales_sorted = daily_sales_resampled.sort_values(by='total_sales', ascending=False).head(10)
Pseudocode:

Create a pivot table with invoice_date as the index and total_sales as values.
Resample the data to daily bins.
Sum the total sales for each day.
Sort the results in descending order.
Select the top 10 days.
7. Determine the Week with the Most Women’s Athletic Footwear Sales
Arguments:

women_footwear_df (DataFrame): Filtered DataFrame with only women’s athletic footwear data.
Returns:

weekly_sales (DataFrame): A DataFrame showing the top 10 weeks with the highest sales for women’s athletic footwear.
Examples:

python
Copy code
# Pivot table for weekly sales
weekly_sales_pivot = women_footwear_df.pivot_table(index='invoice_date', values='total_sales', aggfunc='sum')

# Resampling and sorting
weekly_sales_resampled = weekly_sales_pivot.resample('W').sum()
weekly_sales_sorted = weekly_sales_resampled.sort_values(by='total_sales', ascending=False).head(10)
Pseudocode:

Create a pivot table with invoice_date as the index and total_sales as values.
Resample the data to weekly bins.
Sum the total sales for each week.
Sort the results in descending order.
Select the top 10 weeks..

2. **Main Program Execution:**
   - Load the DataFrame.
   - Apply column renaming transformations.
   - Print the updated DataFrame.

## Features

- **Column Renaming:**
  - Renames columns to reflect more descriptive names for better readability.

- **Monetary Column Formatting:**
  - Updates column names related to monetary values to reflect their unit in millions.

- **DataFrame Update:**
  - Applies renaming transformations directly to the DataFrame.

- **Formatted Output:**
  - Displays the updated DataFrame to verify the applied changes.

## Requirements

- Python 3.6 or later
- Pandas library

## Setup

1. Clone this repository to your local machine:

   ```sh
   git clone https://github.com/sack2116/athletic_sales_analysis.git

2. Navigate to the project directory:

sh
Copy code
cd athletic_sales_analysis
3. Install the required libraries:
4. Launch Jupyter Notebook
Start Jupyter Notebook from the project directory: >>

bash
Copy code
jupyter notebook
This will open Jupyter Notebook in your default web browser.

5. Open the Notebook
In the Jupyter Notebook interface, navigate to the directory where the notebooks are located (usually notebooks or similar). Click on the notebook file (e.g., athletic_sales_analysis.ipynb) to open it.

6. Run the Notebook Cells
Execute each cell in the notebook by clicking the "Run" button or pressing Shift + Enter. Follow the instructions within the notebook to perform the analysis.

