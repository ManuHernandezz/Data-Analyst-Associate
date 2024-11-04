# Practical Exam: Grocery Store Sales

FoodYum is a grocery store chain that is based in the United States. <br> Food Yum sells items such as produce, meat, dairy, baked goods, snacks, and other household food staples. <br> As food costs rise, FoodYum wants to make sure it keeps stocking products in all categories that cover a range of prices to ensure they have stock for a broad range of customers.

## Data
The data is available in the table products. The dataset contains records of customers for their last full year of the loyalty program.

| Column Name | Criteria | 
|--------|-----------|
|product_id|Nominal. <br> The unique identifier of the product. <br> Missing values are not possible due to the database structure.|
|product_type|Nominal. <br> The product category type of the product, one of 5 values (Produce, Meat, Dairy, Bakery, Snacks). <br> Missing values should be replaced with “Unknown”.|
|brand|Nominal. <br>  The brand of the product. One of 7 possible values. <br> Missing values should be replaced with “Unknown”.|
|weight|Continuous. <br> The weight of the product in grams. <br> This can be any positive value, rounded to 2 decimal places. <br> Missing values should be replaced with the overall median weight.|
|price|Continuous.  <br> The price the product is sold at, in US dollars. <br> This can be any positive value, rounded to 2 decimal places. <br> Missing values should be replaced with the overall median price.|
|average_units_sold|Discrete.  <br> The average number of units sold each month.  <br> This can be any positive integer value.  <br> Missing values should be replaced with 0.|
|year_added|Nominal. <br> The year the product was first added to FoodYum stock. <br> Missing values should be replaced with 2022.|
|stock_location|Nominal. <br> The location that stock originates. <br> This can be one of four warehouse locations, A, B, C or D <br> Missing values should be replaced with “Unknown”.|

