

--Get the earliest time the shop closes


--Get the latest time the shop closes
SELECT MAX(transaction_time)
FROM coffee_shop_sales;

--Final Query fo analysis
SELECT 
   SUM(transaction_qty*unit_price) AS total_revenue.
   SUM(transaction_qty) AS number_of_units_sold.
   COUNT(transaction_id) AS number_of_sales.

   TO_DATE(TRANSACTION_DATE)
   TO_CHAR(TRANSACTION_DATE, 'YYYYMM') AS month_id,
   MONTHNAME (TRANSACTION_DATE) AS month_name

   CASE
      WHEN transaction_time BETWEEN "06:00:00" AND "11:59:59" THEN 'Morning'
      WHEN transaction_time BETWEEN "12:00:00" AND "15:59:59" THEN 'Afternoon'
      WHEN transaction_time BETWEEN "16:00:00" AND "20:00:00" THN  'Evening'
      ELSE 'Night'
  END AS time_bucket,

         product_category,
         product_type,
         product_detail,
         store_location
   CASE
      WHEN SUM(transaction_qty*unit_price) BETWEEN 0 AND 20 THEN 'low'
      WHEN SUM(transaction_qty*unit_price) BETWEEN 21 AND 40 THEN 'Med'
      WHEN SUM(transaction_qty*unit_price) BETWEEN 41 AND 60 THEN  'High'
      ELSE 'Very High'
      END AS spend_bands,
     
  FROM coffee_shop_sales  
  GROUP BY time_bucket,
           product_category,
           product_type,
           product_detail,
           store_location,
           month_id,
           month_name,
           day_name,
 --(dont end in group by because its already there(not aggregate))
         
