# SQL-Retail_sales_project1

create database sql_project1;
use sql_project1;

create table retail_sales ( transactions_id int primary key,
sale_date date, sale_time time, customer_id int, gender varchar(10),
age int, category varchar(15), quantiy int,
price_per_unit float, cogs float, total_sale float
);

# Data cleaning-------------------------------------------
select * from retail_sales;
SELECT COUNT(*) AS total_rows FROM retail_sales;

 # rename the column
ALTER TABLE retail_sales 
change quantiy quantity int;

# Check the columns have nulls
select * from retail_sales
where 
transactions_id is null 
or
sale_time is null
 or
sale_date is null
or
gender is null
 or 
 category is null
 or 
 quantity is null
 or 
 price_per_unit is null
or 
cogs is null
or 
total_sale is null; 

# delete the null values
delete from retail_sales 
where 
transactions_id is null 
or
sale_time is null
 or
sale_date is null
or
gender is null
 or 
 category is null
 or 
 quantity is null
 or 
 price_per_unit is null
or 
cogs is null
or 
total_sale is null; 

# check the total no of columns
select count(*) from retail_sales;

# data exploration--------------------------------------------------

# how many sales we have?
select count(*) as total_sales from retail_sales;

# how many customers we have ?
select count(customer_id) as Total_customers from retail_sales;

# how many unique customers we have ?
select count(distinct(customer_id)) as Total_customers from retail_sales;

-- Data Analysis & Business Key Problems & Answers

-- My Analysis & Findings
1. **Write a SQL query to retrieve all columns for sales made on '2022-11-05'**: 
 '''sql 
select * from retail_sales
 where sale_date = '2022-11-05';
'''
 
2. **Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4 in the month of Nov-2022**: 
 '''sql 
select * from retail_sales 
where category = 'Clothing' 
and quantity >= 4
and sale_date between '2022-11-01' and '2022-11-30';
 '''

3. **Write a SQL query to calculate the total sales (total_sale) for each category**: 
 '''sql 
select category, sum(total_sale)as Total_sales, 
count(*) as total_orders from retail_sales
group by 1;
'''

4. **Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category**: 
 '''sql 
select round(avg(age)) as Avg_age from retail_sales
where category ='Beauty';
select * from retail_sales;
'''
 
5. **Write a SQL query to find all transactions where the total_sale is greater than 1000**: 
 '''sql 
select * from retail_sales
where total_sale > 1000;
'''

6. **Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category**: 
 '''sql 
select category,gender, count(*) as Total_No from retail_sales
group by 1,2
order by 1;
'''
 
7. **Write a SQL query to calculate the average sale for each month. Find out best selling month in each year**: 
 '''sql 
select year(sale_date) as Year, month(sale_date) as Month, sum(total_sale) as Total_sale from retail_sales
group by 1, 2 
order by 1,2 desc;
 '''
 
8. **Write a SQL query to find the top 5 customers based on the highest total sales**: 
 '''sql 
select  customer_id, sum(total_sale)from retail_sales 
group by 1
order by 2 desc
limit 5;
''' 
 
9. **Write a SQL query to find the number of unique customers who purchased items from each category )**: 
 '''sql
select  category ,count(distinct(customer_id)) as total_no from retail_sales
group by 1;
'''

10. **Write a SQL query to create each shift and number of orders (Example Morning <=12, Afternoon Between 12 & 17, Evening >17)**: 
 '''sql
SELECT *,
CASE
    WHEN HOUR(sale_time) < 12 THEN 'Morning'
    WHEN HOUR(sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
    ELSE 'Evening'
END AS shift
FROM retail_sales;
'''
**End of project**
 
## Findings

- **Customer Demographics**: The dataset includes customers from various age groups, with sales distributed across different categories such as Clothing and Beauty.
- **High-Value Transactions**: Several transactions had a total sale amount greater than 1000, indicating premium purchases.
- **Sales Trends**: Monthly analysis shows variations in sales, helping identify peak seasons.
- **Customer Insights**: The analysis identifies the top-spending customers and the most popular product categories.

## Reports

- **Sales Summary**: A detailed report summarizing total sales, customer demographics, and category performance.
- **Trend Analysis**: Insights into sales trends across different months and shifts.
- **Customer Insights**: Reports on top customers and unique customer counts per category.

## Conclusion
- **This project serves as a comphrensive introduction to SQL for data analysts, covering database setup, data cleaning, exploratory data analysis, and bsuiness driven SQL queries. 
- **The findings from this project can help drive business decisions by understanding sales patterns, customer behaviour, and product performance.
