# Pizza-Sales-Analysis
## Table of contents
## Glossary
- KPI: Key Point Indicators are metrics that measure the business's success.
- Exploratory Data Analysis: The main purpose of EDA is to help look at data before making any assumptions. It can help identify obvious errors, as well as better understand patterns within the data, detect outliers or uncommon events, and find interesting relations among the variables.
- Revenue: the total amount of money generated by the business
## project overview
The project's objective is to help look at the trends in the dataset; followed by comparing which pizza type and size brings in the most sales and lastly looking at the best and worst sellers in the pizza dataset. Additionally, the data source is a CSV file but KPI questions are answered firstly with SQL then Excel with each metric for the pizzeria being visualized. Lastly, the insights from the analysis will be explained with recommendations given.
## Dashboard
![Pizza Sales Dashboard](https://github.com/Tyroneekhator/Pizza-Sales-Analysis/assets/72547969/f5955811-a941-4c19-ae25-05103408790e)

## Data Sources Used
- A CSV file
## Columns in the dataset
- Pizza_id: the unique identifier of each pizza ordered.
- Order_id: the distinct code of each order made by a customer.
- Total_orders: the column that allows one to get the total orders from the data set
- Pizza_name_id: the distinctive way of identifying the name of each pizza. That is "pizza name_size of pizza"
- Quantity: number of times specific pizzas are ordered.
- Order date: when the pizza was ordered.
- Order time: the time it is ordered.
- Order day: the day of the week it was ordered
- Order month: the month of the year it was ordered
- Order hour: the hour of the day it was ordered
- Order year: The year it was ordered
- Unit price: the price of each pizza sold
- total price: the unit price * quantity
- Pizza size: the size of the pizza
- Pizza category: category of the pizza
- pizza ingredients: the ingredients that make up the pizza
- pizza name: the name of the pizza
## Tools Used
- SQL: Structured Query Language is a domain-specific language used to manage data, especially in a relational database management system. It is beneficial in handling structured data, i.e., data incorporating relations among entities and variables
- Excel: A spreadsheet software
## Data cleaning and transformation process
### Data SQL Process
1. CSV file which shall be put in SQL Server Management Studio
2. Create a new database
3. Import flat file
4. Change data types
   - nvarchar(50) ---> varchar(50)
   - pizza_ingredients nvarchar(50)  ---> varchar(200)
   - pizza_id small init to init
   - Order_id small init to init
### Data cleaning in Excel
1. Change column values
     - S - Small
     - M - Medium
     - L - Large
     - XL - Extra large
     - XXL - Extra Extra Large
  - Method uses the IFS statement function in the helper column
  - Copy and paste values in the original column then delete the helper column.
## Key point indicators requirements in SQL and Excel
These are the questions that need to be answered to measure the success rate of the business.
1. Total revenue: The sum of the total price of all pizza orders.
2. Average Order Value: the average amount spent per order, calculated by dividing the total revenue by the total number of orders
3. Total pizzas sold: The sum of the quantities sold.
4. Total orders: The total number of orders placed.
5. Average pizzas per order: The average number of pizzas sold per order, is calculated by dividing the total number of pizzas sold by the total number of orders.
6. Total number of orders placed by days of the week.
7. Hourly trend for numbers of pizzas ordered.
8. Percentage of sales by pizza category.
9. Percentage of sales by pizza size.
10. Total pizzas sold by pizza category.
11. Top 5 best sellers by total pizzas sold.
12. Top 5 worst sellers by total pizzas sold.
## Insights gotten via SQL
show the SQL queries written to answer KPI requirements. A Word document version will be provided
1. Total Revenue: Total sum of the total price of all pizza orders.
   - -- SQL query to get total revenue: the sum price of all the pizzas ordered.<br /><br />
         SELECT SUM(total_price) AS Total_Revenue <br />
         FROM pizza_sales <br /> <br /> ![Screenshot (447)](https://github.com/Tyroneekhator/Pizza-Sales-Analysis/assets/72547969/cec98c7e-a67b-4a69-bbaf-b9aa6ab43573)
2. Average order Value: The average amount spent per order, calculated by dividing the total revenue by the total number of orders.
   - -- SQL query to get the average spent per order: Average order Value That is the average amount spent per order <br /><br />
      SELECT SUM(total_price)/ COUNT(DISTINCT order_id) AS Average_Order_Price <br />
      FROM pizza_sales <br /> ![Screenshot (448)](https://github.com/Tyroneekhator/Pizza-Sales-Analysis/assets/72547969/6b855c01-a926-4c6e-acd1-914d8c8cd0a6)
3. Total Pizzas Sold: The Sum of the quantities of all pizzas sold. 
- -- SQL query total pizzas sold: The sum of the qualities of all of the pizzas sold<br /> <br />
      SELECT SUM(quantity) as Total_Pizza_Sold<br />
      FROM pizza_sales <br />![Screenshot (449)](https://github.com/Tyroneekhator/Pizza-Sales-Analysis/assets/72547969/b49d8507-8a38-479c-9b45-37b8d6491a79)
4. Total Orders: The total number of orders placed. <br />
- -- SQL query total orders: The total number of orders placed. <br /> <br />
SELECT COUNT(DISTINCT order_id) as total_numbers_of_orders_placed <br />
FROM pizza_sales <br />![Screenshot (450)](https://github.com/Tyroneekhator/Pizza-Sales-Analysis/assets/72547969/966f4c1e-cf0e-4dde-80b8-be690a1df0d6)
5. Average Pizzas Per Order: The average number of pizzas sold per order, is calculated by dividing the total number of pizzas sold by the total number of orders.
  - -- SQL query Average Pizzas Per Order: The average number of pizzas sold per order <br /> <br />
      SELECT SUM(Quantity)/COUNT(DISTINCT order_id) as average_number_of_pizza_sold_per_order<br />
      FROM pizza_sales<br />![Screenshot (451)](https://github.com/Tyroneekhator/Pizza-Sales-Analysis/assets/72547969/26a59cc6-b998-40f0-80c5-af23b4c0cbdb)
6.	Total number of orders placed by days of the week.
- -- SQL query total number of orders by days of the week <br /><br />
SELECT DATENAME(DW,order_date) as order_day,COUNT(DISTINCT order_id) AS Total_Orders<br />
FROM pizza_sales<br />
GROUP BY DATENAME(DW,order_date)<br />![Screenshot (452)](https://github.com/Tyroneekhator/Pizza-Sales-Analysis/assets/72547969/a7c6442b-004e-4a63-8de0-eb9822287d50)
7. Hourly trend for  the number of pizzas ordered.
- -- SQL query for hourly trend of pizzas ordered<br /><br />
SELECT DATEPART(HOUR,order_time) as order_hours,COUNT(DISTINCT order_id) AS Total_Orders<br />
FROM pizza_sales<br />
GROUP BY DATEPART(HOUR,order_time)<br />
ORDER BY DATEPART(HOUR,order_time)<br />
![Screenshot (454)](https://github.com/Tyroneekhator/Pizza-Sales-Analysis/assets/72547969/2bf10f08-4ed9-47f4-883c-a7e6d399d5cb)
8.	Percentage of sales by pizza category
-- SQL query for percentage of sales by pizza category<br /><br />
      SELECT pizza_category,SUM(total_price)* 100/(SELECT sum(total_price) FROM pizza_sales) AS Percentage_Total<br />
      FROM pizza_sales<br />
      GROUP BY pizza_category<br />![Screenshot (453)](https://github.com/Tyroneekhator/Pizza-Sales-Analysis/assets/72547969/bdac269e-bcba-407d-9c61-3becc0472ccd)
  
9.	Percentage of Sales by Pizza Size<br />
-- SQL query for percentage of sales by pizza size<br /><br />
SELECT pizza_size,SUM(total_price) as total_revenue,SUM(total_price)*100/(SELECT SUM(total_price) From pizza_sales) AS percentage_total<br />
FROM pizza_sales<br />
GROUP BY pizza_size<br />
![Screenshot (456)](https://github.com/Tyroneekhator/Pizza-Sales-Analysis/assets/72547969/a2c0ff92-c597-438b-9293-5c001e1cf98d)






      




      






## Recommendations based on the analysis
