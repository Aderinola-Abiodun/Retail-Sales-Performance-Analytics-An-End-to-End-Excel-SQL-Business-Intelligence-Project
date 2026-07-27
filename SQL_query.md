## SQL Exploratory Data Analysis Summary

After cleaning and validating the dataset in Excel, the data was imported into PostgreSQL for exploratory data analysis (EDA). The objective of this phase was to transform raw transactional data into meaningful business insights by answering key operational, financial, and customer-focused questions.

Using SQL, I conducted a comprehensive analysis covering **50 business questions**, ranging from basic data exploration to advanced analytical techniques. The analysis examined sales performance, customer demographics, purchasing behavior, profitability, shipping efficiency, customer satisfaction, product performance, and regional trends. Advanced SQL concepts such as **Common Table Expressions (CTEs)**, **window functions** (`RANK()`, `DENSE_RANK()`, `LAG()`, and `NTILE()`), **aggregate functions**, **CASE statements**, and **subqueries** were applied to uncover trends, rank performance, calculate growth, segment customers, and generate actionable business insights.

### Key Project Highlights

* Analyzed **4,280 sales transactions** across **4,112 unique customers**.
* Explored business performance across **20 cities**, **5 regions**, and **42 unique products**.
* Calculated key business metrics, including total revenue, total profit, average order value, shipping performance, customer satisfaction, and return rates.
* Identified top-performing products, categories, customers, cities, and regions based on revenue and profitability.
* Evaluated customer purchasing behavior, discount strategies, payment preferences, and product return patterns.
* Assessed operational efficiency by analyzing shipping times, order status, and delivery performance.
* Applied advanced SQL techniques to rank products, measure regional sales contributions, calculate month-over-month sales growth, identify high-value customers, and build customer spending segments.

The findings from this analysis provide management with valuable insights to optimize pricing strategies, improve operational efficiency, enhance customer satisfaction, increase profitability, and support data-driven decision-making.
```SQL
Create Table sales
(order_id Text,
Order_month Varchar(20),
Order_year INT,
customer_id	Text, 
customer_name	Varchar(100),
age	INT,
gender Varchar(20),
region Varchar(20),
city Varchar(20),
product_category varchar(150),
product_name Varchar(150),
quantity	INT,
unit_price decimal(10, 2),
discount_pct decimal(10, 2),
sales_amount decimal(10, 2),
profit	decimal(10, 2),
shipping_cost decimal(10, 2),
payment_method Varchar(150),
customer_satisfaction Text,
return_flag	boolean,
order_status Varchar(150),
days_to_ship Text
);

-- checking the whole data set after cleaning. 

select * from sales; 

-- Data Exploration 
-- Question 1- How many orders were placed?
select count(*) as total_orders from sales;--  there are 4280 orders 

-- Question 2- How many unique customers does the company have?
select count(distinct customer_id) as total_count from sales;-- there are 4112 unique customers

-- Question 3- How many cities does the company operate in?
select count( distinct city) from sales; -- the company operates in 20 different cities


-- Question 4- How many regions are represented?
select count(distinct region) as count_of_region from sales; -- there are 5 different regions 

-- Question 5- What product categories exist?
select product_category, count(*) as total_count from sales
group by 1;-- the total product categories that exist and their count

-- Question 6 - How many unique products are sold?
select count(distinct Product_name) as total_unique_product from sales;
-- There are a total of 42 unique products sold 

-- Question 7- What is the average customer age?
select round(avg(age), 2) as average_age from sales; 
-- The average customer age from the data set is 35.34

--  Question 8 - What percentage of customers are male and female?
select gender, round(count(*) * 100 / sum(count(*)) over(), 2) as percentage from sales
group by 1;-- so the percentage of male is 33.69 %, female is 32.62 % and others 33.69%

-- Question 9 -Which payment methods are used?
select payment_method, count(*) as total_count from sales
group by 1-- the following are the payment methods from the data set: UPI, Net Banking, EMI, DEbit Crad, Cash on Delivery, and Credit Card


-- Question 10 - How many returned orders exist?
select Order_status, count(*) as total_count from sales
group by 1
having order_status = 'Returned'; -- Returned orders are 623


-- Sales Performance
-- Question 11- What is the total sales revenue?
select sum(sales_amount) as total_sales_revenue from sales; -- the total profit is 266,894,969.01 USD

-- Question 12- What is the total profit?
select sum(profit) as total_sales_revenue from sales; -- the total profit is 50,020,895.23 USD

-- Question 13- What is the average order value?
select round(avg(sales_amount), 2) as average_order_value from sales; 
-- The average order value is 62,358.64

-- Question 14- Which month generated the highest sales?
select order_month, Sum(sales_amount) as month_generated from sales
group by 1
order by 2 desc; -- the following are the months and their revenue 


-- Question 15 - Which year recorded the highest revenue?
select order_year, sum(sales_amount) as year_generated from sales
group by 1
order by 2 desc
LIMIT 1; -- the highest year, which revenue is 2023

-- Question 16 - Which region generated the highest sales?
select Region, sum(sales_amount) as amount_generated from sales
group by 1
order by 2 desc
limit 1; -- The South region generated the highest amount of revenue 

-- Question 17 - Which city generated the highest revenue?
select city, sum(sales_amount) as amount_generated from sales
group by 1
order by 2 desc
limit 1;-- Kochii is the city with the highest generated revenue 

-- Question 18- Which product category generated the highest revenue?
select product_category, sum(sales_amount) as amount_generated from sales
group by 1 
order by 2 desc 
LIMIT 1; -- Electronics is the product category with the highest revenue 


-- Question 19- Which product generated the highest revenue?
select product_name, sum(sales_amount) as amount_generated from sales 
group by 1
order by 2 desc 
LIMIT 1; -- tablet is the product with the highest generated revenue

-- Question 20 - Which products sold the highest quantity?
select product_name, sum(quantity) as highest_quantity from sales
group by 1
order by 2 desc
LIMIT 1; -- rice is the highest quantity of product sold

-- Section C Customer Analytics
-- Question 21- Who are the Top 10 customers by sales?
select customer_name, sum(sales_amount) as sales_amount from sales
group by 1
order by 2 desc
LIMIT 10; 

-- Question 22 - Who are the Top 10 customers by profit?
select customer_name, sum(profit) as total_profit from sales
group by 1
order by 2 desc
LIMIT 10; 

-- Question 23: Which age group spends the most?
select age, sum(sales_amount) as total_sale_amount from sales
group by 1
having age <= 100
order by 2 desc
limit 1; --36 is the highest age group that spends the most across all cities

-- Question 24- Does gender influence purchasing behavior?
select gender, sum(sales_amount) as total_sales_amount from sales
group by 1
order by 2 desc; --yes gender influences purchase behaviour 

-- Question 25 - Which region has the most loyal customers (repeat purchases)?
select region, customer_name, count(*) as total_customers from sales
group by 1, 2
order by 3 desc; -- The West is the region with the most loyal customers

-- Question 26 - Which customers receive the highest discounts?
select customer_name, sum(discount_pct) as highest_discount from sales
group by 1
order by 2 desc 
LIMIT 1; -- Meera Kumar is the customer with the highest discount

-- Profitability
-- Question 27- Which products generate the highest profit?
select product_name, sum(profit) as total_profit from sales
group by 1
order by 2;

-- Question 28- Which products generate losses?
select Product_name,  from sales; 

-- Question 29- Which categories have the highest profit margin?
select product_category, sum(profit) as total_profit from Sales
group by 1
order by 2 desc; 

-- Question 30 - Which cities generate the highest average profit?
select city, round(avg(profit), 2) as average_profit from sales
group by 1
order by 2 desc
LIMIT 3; -- the following cities have generated the highest average profit, which include: Kochi, Amritsar, and Chennai

-- Question 31- How much profit is lost through discounts?
with CTE as (select sum(profit) as total_profit, sum(discount_pct) as total_discount  from sales)
select Total_profit - total_discount as profit_lost_through_discount from CTE; 

-- Question 32: Is there a relationship between discount percentage and profit?
select sum(profit) as total_profit, sum(discount_pct) as total_discount  from sales; 
-- there is a major difference between discount percentage and profit 

-- Shipping & Operations
-- Question 33 - What is the average shipping time?

-- convert days to ship to numeric first 
alter table sales
alter column days_to_ship type INT
USING days_to_ship::integer; 

-- Question
select round(avg(days_to_ship), 2) as average_shipping_time from sales; 
-- The average shipping time is 5.62

-- Question 34- Which regions experience the longest shipping times?
select region, sum(days_to_ship) as shipping_time from sales
group by 1
order by 2 desc; -- the south as the longest shipping time 

-- Question 35 - Which products take the longest to ship?
select product_name, sum(days_to_ship) as total_shipping_time from sales
group by 1
order by 2 desc
LIMIT 3; -- these are the three products with the longest time to ship 

-- Question 36- Does longer shipping lead to more product returns?
SELECT days_to_ship,
        CASE
            WHEN order_status = 'Returned' THEN 1
            ELSE 0
        END AS Total_Returns
FROM sales
order by 1 desc; -- No. Longer shipping doesn't mean more product returns 

-- Question 37- Which order status occurs most frequently?
select order_status, count(*) as total_number_of_count from sales
group by 1
order by 2 desc
LIMIT 1; 

-- Customer Experience
-- Question 38- What is the average customer satisfaction score?

--Changing the type 
alter table sales
alter column customer_satisfaction type INT
USING customer_satisfaction::integer;

select round(avg(customer_satisfaction), 2) as average_customer_satisfaction from sales; 
-- The average customer satisfaction is 3.02

-- Question 39- Which cities have the highest customer satisfaction?
select city, sum(customer_satisfaction) as total_customer_satisfaction from sales
group by 1
order by 2 desc; 

-- Question 40- Are returned products associated with lower customer satisfaction?
select order_status, sum(customer_satisfaction) customer_satisfaction from sales
group by 1
having order_status = 'Returned' 
-- No returned Products are not assocuated with lower customer satisfaction 

-- Bonus Advanced SQL Questions (Highly Recommended)
-- Question 41- Rank products by total revenue using RANK().
SELECT
    product_name,
    SUM(sales_amount) AS total_sales,
    RANK() OVER (
        ORDER BY SUM(sales_amount) DESC
    ) AS sales_rank
FROM sales
GROUP BY product_name;; 

-- Question 42- Find the Top 3 products within each category using DENSE_RANK().
with CTE as (SELECT
    product_category,
    product_name,
    SUM(sales_amount) AS total_sales,
    DENSE_RANK() OVER (
        PARTITION BY product_category
        ORDER BY SUM(sales_amount) DESC
    ) AS rank_in_category
FROM sales
GROUP BY product_category, product_name)
SELECT * from CTE 
where rank_in_category <= 3;

-- Question 43- Calculate each region's contribution to total company sales.
SELECT
    region,
    SUM(sales_amount) AS total_sales,
    ROUND(
        SUM(sales_amount) * 100.0 /
        SUM(SUM(sales_amount)) OVER (),
        2
    ) AS percentage
FROM sales
GROUP BY region;


-- Question 44- Calculate month-over-month sales growth using LAG().
WITH monthly AS (
  SELECT order_month, order_year, SUM(sales_amount) AS total_sales
  FROM sales
  GROUP BY order_month, order_year
)
SELECT 
  order_month,
  order_year,
  total_sales,
  LAG(total_sales) OVER (ORDER BY order_year, order_month) AS prev_month_sales,
  ROUND((total_sales - LAG(total_sales) OVER (ORDER BY order_year, order_month)) * 100.0 /
    NULLIF(LAG(total_sales) OVER (ORDER BY order_year, order_month), 0), 2) AS growth_pct
FROM monthly;

-- Question 45- Identify customers whose spending is above the company average.
with CTE as (select customer_name, sum(sales_amount) as total_amount from sales
group by 1)
Select * from CTE 
where total_amount > (select avg(sales_amount) from sales);

-- Question 46- Calculate cumulative sales over time.
select order_month, sum(sales_amount) over(partition by order_month) as cumulative_sales from sales
order by 2 desc; 

-- Question 47- Identify the top 20% of customers contributing to total revenue using NTILE().
with CTE as (SELECT *,
       NTILE(100) OVER (ORDER BY sales_amount DESC) AS percentile
FROM sales)
select * from CTE 
where Percentile <= 20;

-- Question 48- Calculate profit margin for every product and rank them.
with CTE as (select product_name, sum(sales_amount) as total_sum from sales
group by 1)
select *, rank() over(partition by product_name order by total_sum desc) from CTE; 

-- Question 49- Find products whose sales are above the category average.
with ONE as (select product_name, sum(sales_amount) as total_sales from sales
group by 1),
TWO as (select product_name, product_category, round(avg(sales_amount), 2) as average_sales from sales
group by 1, 2)
select o.product_name, o.total_sales, t.average_sales from Two as T
join one as o 
on o.product_name = t.product_name
where  o.total_sales > t.average_sales; 


-- Question 50- Create customer segments based on total spending: Bronze, Silver, Gold, Platinum

select *, case when sales_amount < 3000 then 'Bronze' 
when sales_amount between 3001 and 15000 then 'Silver'
when sales_amount between 15001 and 30000 then 'Gold'
else 'Platinum' 
end as Customer_segments from sales; 

-- the count of cities in the data set 
select count(distinct city)from sales; 


