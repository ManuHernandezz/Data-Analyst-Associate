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

## Task 1

Last year (2022) there was a bug in the product system. For some products that were added in that year, the year_added value was not set in the data. As the year the product was added may have an impact on the price of the product, this is important information to have.

Write a query to determine how many products have the year_added value missing. Your output should be a single column, missing_year, with a single row giving the number of missing values.

```sql
SELECT COUNT(*) AS missing_year_added
FROM public.products
WHERE public.products.year_added IS NULL
```

## Task 2

Given what you know about the year added data, you need to make sure all of the data is clean before you start your analysis. The table below shows what the data should look like.

Write a query to ensure the product data matches the description provided. Do not update the original table.


```sql
SELECT product_id,
		COALESCE(NULLIF(REPLACE(product_type,'-',''),''),'Unknown') AS product_type,
		COALESCE(NULLIF(REPLACE(brand,'-',''),''),'Unknown') AS brand,
		COALESCE(
        	ROUND(CAST(REPLACE(weight, ' grams', '') AS NUMERIC), 2),
        	(SELECT PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY CAST(REPLACE(weight, ' grams', '') AS NUMERIC)) FROM products)) AS weight,
		COALESCE(
        	ROUND(CAST(price AS NUMERIC), 2),
        	(SELECT PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY price) FROM products)) AS price,
		COALESCE(year_added,'2022') AS year_added,
		UPPER(COALESCE(stock_location, 'Unknown')) AS stock_location
FROM products
```

## Task 3

To find out how the range varies for each product type, your manager has asked you to determine the minimum and maximum values for each product type.

Write a query to return the product_type, min_price and max_price columns.
```sql
SELECT product_type,
	MIN(price) AS min_price,
	MAX(price) AS max_price
FROM products
GROUP BY product_type
```


## Task 4

The team want to look in more detail at meat and dairy products where the average units sold was greater than ten.

Write a query to return the product_id, price and average_units_sold of the rows of interest to the team.
```sql
SELECT product_id, price, average_units_sold
FROM products
WHERE product_id IN (
    SELECT product_id
    FROM products
    WHERE 
        product_type IN ('Meat', 'Dairy')
        AND average_units_sold > 10
)
ORDER BY average_units_sold DESC;
```

