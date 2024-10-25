# Pizza-Sales-Analysis
SQL queries used to analyze pizza sales data.
# Problem Statement

## A. KPI's Requirement
-**We need to analyze key indicators for our piuzza sales data to gain insights into our buisness performance. Specifically, we wanto to calculate the following metrics**

#### 1. Total Revenue
The sum of the total price of all pizzas orders.

#### Query:
SELECT 
    SUM(total_price) AS total_revenue
FROM
    pizza_sales;

#### Output:
![image](https://github.com/user-attachments/assets/184fd7b2-8e79-46ed-a82d-97954b0d37ca)

#### 2. Average Order Value
The average amount spent per order, calculated by dividing the total revenue by the total nuber of orders.

#### Query:
SELECT 
    (SUM(total_price) / COUNT(DISTINCT order_id)) AS avg_order_value
FROM
    pizza_sales;

#### Output:
![image](https://github.com/user-attachments/assets/b9afc423-8896-4991-9c17-55e6350812a8)

#### 3. Total Pizza Sold
The sum of quanties of all pizzas sold.

#### Query:
  SELECT 
    SUM(quantity) AS total_pizza_sold
FROM
    pizza_sales;

#### Output:
![image](https://github.com/user-attachments/assets/fb10cb30-51c7-4727-8343-36d623b7ed1c)

#### 4. Total Orders
The total number of orders placed.

#### Query:
SELECT 
    COUNT(DISTINCT order_id) AS total_orders
FROM
    pizza_sales;

#### Output:
![image](https://github.com/user-attachments/assets/9f1ef44f-887f-44a3-b168-15e2fe08cdf9)

#### 5. Average Pizzas Per Order
The average number of pizzas sold per order, calculated by dividing the total number of pizzas sold by the total number of orders.

#### Query:
 SELECT 
    ROUND((SUM(quantity) / COUNT(DISTINCT order_id)),
            2) AS avg_pizzas_per_order
FROM
    pizza_sales;
    
#### Output:
![image](https://github.com/user-attachments/assets/09eb5bf5-34af-4a29-a434-a82f19ebf59d)

#### B. Daily Trend for Total Orders
The below query will help us to identify any patters or fluctuations in order volumes on a daily basis.

#### Query:
SELECT 
    DATE_FORMAT(order_date, '%a') AS order_day,
    COUNT(DISTINCT order_id) AS total_orders
FROM
    pizza_sales
GROUP BY order_day;

#### Output:
![image](https://github.com/user-attachments/assets/f1a64e8c-8b70-4329-a441-00133b9ad517)

#### C. Monthly Trend for Orders
The below query will allow us to identify periods of high order activity.

#### Query:
SELECT 
    DATE_FORMAT(order_date, '%M') AS Month_Name,
    COUNT(DISTINCT order_id) AS total_orders
FROM
    pizza_sales
GROUP BY Month_Name;

#### Output:
![image](https://github.com/user-attachments/assets/be778f51-4334-4689-91af-69a267b9eaeb)

#### D. Percentage of Sales by Pizza Category
The below query will provide insights into popularity of various pizza categories and their contribution to overall sales.

#### Query:
SELECT 
    pizza_category,
    ROUND(SUM(total_price), 2) AS total_revenue,
    ROUND(SUM(total_price) * 100 / (SELECT 
                    SUM(total_price)
                FROM
                    pizza_sales),
            2) AS PCT
FROM
    pizza_sales
GROUP BY pizza_category;

#### Output:
![image](https://github.com/user-attachments/assets/8a081fbe-9c0f-4a30-b576-d476a6d44fb6)

#### E. Percentage of Sales by Pizza Size
The below query will help us to understand customer preferences for pizza size and their impact on sale.

#### Query:
SELECT 
    pizza_size,
    ROUND(SUM(total_price), 2) AS total_revenue,
    ROUND(SUM(total_price) * 100 / (SELECT 
                    SUM(total_price)
                FROM
                    pizza_sales),
            2) AS PCT
FROM
    pizza_sales
GROUP BY pizza_size;

#### Output:
![image](https://github.com/user-attachments/assets/c542ad17-520d-4c5c-95b6-4d377bc0e952)

#### F. Total Pizzas Sold by Pizza Category 
The below query will allow us to compare sales performance of different pizza categories.

#### Query:
SELECT 
    pizza_category, SUM(quantity) AS total_qty_sold
FROM
    pizza_sales
GROUP BY pizza_category
ORDER BY total_qty_sold DESC;

#### Output:
![image](https://github.com/user-attachments/assets/0c42b219-bc62-4aa5-9624-b58bf1b722d5)

#### G. Top 5 Best Sellers by Revenue, Total Quantity and Total Orders
The below query will help us to identify the most popular pizza options.

#### G-1. Top 5 Pizzas by Revenue Query:
SELECT 
    pizza_name, SUM(total_price) AS total_revenue
FROM
    pizza_sales
GROUP BY pizza_name
ORDER BY total_revenue DESC
LIMIT 5;

#### Output:
![image](https://github.com/user-attachments/assets/f325a383-5591-46d0-a12e-154b3ab351f1)

#### G-2. Top 5 Pizzas by Quantity Query:
SELECT 
    pizza_name, SUM(quantity) AS total_pizza_sold
FROM
    pizza_sales
GROUP BY pizza_name
ORDER BY total_pizza_sold DESC
LIMIT 5;

#### Output:
![image](https://github.com/user-attachments/assets/06ec5084-373a-437e-8a29-6d896aeffbba)

#### G-3. Top 5 Pizzas by Total Orders Query:
SELECT 
    pizza_name, count(distinct order_id ) AS total_orders
FROM
    pizza_sales
GROUP BY pizza_name
ORDER BY total_orders DESC
LIMIT 5;

#### Output:
![image](https://github.com/user-attachments/assets/979aa60c-e067-4ffa-bd92-c273a42a2f33)

#### H. Bottom 5 Best Sellers by Revenue, Total Quantity and Total Orders
The below query will enable us to identify underperforming or less popular pizza options.

#### H-1. Bottom 5 Pizzas by Revenue Query:
SELECT 
    pizza_name, ROUND(SUM(total_price), 2) AS total_revenue
FROM
    pizza_sales
GROUP BY pizza_name
ORDER BY total_revenue
LIMIT 5;

#### Output:
![image](https://github.com/user-attachments/assets/33d9cfa4-1301-432f-9323-d38fbce555ac)

#### H-2. Bottom 5 Pizzas by Quantity Query:
SELECT 
    pizza_name, SUM(quantity) AS total_pizza_sold
FROM
    pizza_sales
GROUP BY pizza_name
ORDER BY total_pizza_sold
LIMIT 5;

#### Output:
![image](https://github.com/user-attachments/assets/fd0d1ba3-cf47-4daa-ad72-5c205320dc61)

#### H-3. Bottom 5 Pizzas by Total Orders Query:
SELECT 
    pizza_name, COUNT(DISTINCT order_id) AS total_orders
FROM
    pizza_sales
GROUP BY pizza_name
ORDER BY total_orders
LIMIT 5;

#### Output:
![image](https://github.com/user-attachments/assets/04fbb8ee-64b6-45e8-82f5-824489e5695c)

### Software Used:
MySQL



