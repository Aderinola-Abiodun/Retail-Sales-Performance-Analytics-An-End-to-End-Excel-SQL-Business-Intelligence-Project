**Business Problem**

Senior management wants answers to several critical questions:

1. Are sales actually growing every year?
2. Which regions generate the highest profits?
3. Which products drive revenue but reduce profitability?
4. Which customers generate the most lifetime value?
5. How do discounts affect profit?
6. Which payment methods are most popular?
7. What causes product returns?
8. Which cities have the highest customer satisfaction?
9. Which products experience delayed shipping?
10. Which categories should receive more investment?


## Dataset Description

The dataset contains transactional sales records from a retail and e-commerce business, capturing information on customer demographics, product purchases, sales performance, profitability, shipping operations, and customer experience. Each record represents a single customer order and provides the necessary information to analyze business performance, customer behavior, operational efficiency, and financial outcomes.

The dataset consists of the following variables:

| **Column**                | **Description**                                                                                         |
| ------------------------- | ------------------------------------------------------------------------------------------------------- |
| **order_id**              | A unique identifier assigned to each customer order.                                                    |
| **order_month**           | The month in which the order was placed, derived from the order date to support monthly trend analysis. |
| **order_year**            | The year in which the order was placed, enabling year-over-year performance analysis.                   |
| **customer_id**           | A unique identifier assigned to each customer.                                                          |
| **customer_name**         | The full name of the customer who placed the order.                                                     |
| **age**                   | The customer's age at the time of purchase.                                                             |
| **gender**                | The customer's gender.                                                                                  |
| **region**                | The geographical region where the purchase was made.                                                    |
| **city**                  | The city in which the order was placed.                                                                 |
| **product_category**      | The category to which the purchased product belongs.                                                    |
| **product_name**          | The name of the purchased product.                                                                      |
| **quantity**              | The number of units purchased in a single order.                                                        |
| **unit_price**            | The selling price of a single unit of the product before any discounts.                                 |
| **discount_pct**          | The percentage discount applied to the product.                                                         |
| **sales_amount**          | The total revenue generated from the transaction after applying the discount.                           |
| **profit**                | The profit earned from the transaction after accounting for costs.                                      |
| **shipping_cost**         | The cost incurred to deliver the order to the customer.                                                 |
| **payment_method**        | The payment method used by the customer (e.g., Credit Card, Cash, Bank Transfer).                       |
| **customer_satisfaction** | The customer's satisfaction rating or feedback score following the purchase.                            |
| **return_flag**           | Indicates whether the purchased product was returned (`TRUE`) or not (`FALSE`).                         |
| **order_status**          | The current status of the order, such as Delivered, Pending, Cancelled, or Shipped.                     |
| **days_to_ship**          | The total number of days taken to ship and deliver the customer's order.                                |

This dataset provides a comprehensive view of the company's sales operations and serves as the foundation for analyzing revenue trends, customer purchasing behavior, product performance, profitability, shipping efficiency, payment preferences, return patterns, and overall business performance using SQL and Excel.

## Data Cleaning and Preparation

Before conducting any analysis, the dataset underwent a comprehensive data cleaning and preparation process in Microsoft Excel to improve its quality, consistency, and reliability. The objective was to ensure that the data was accurate, standardized, and ready for import into PostgreSQL for further analysis.

The following data cleaning steps were performed:

1. **Handled Missing Values:** Replaced all missing values in the **Shipping Cost** column with the column's average value (mean imputation) to maintain data completeness while minimizing the impact of missing records.

2. **Standardized Text Formatting:** Converted all relevant text fields to **Proper Case** to ensure consistency across customer names, product names, cities, regions, and other categorical variables.

3. **Created Additional Features:** Derived two new columns—**Order Month** and **Order Year**—from the **Order Date** column to support time-based analysis and trend reporting.

4. **Removed Duplicate Records:** Identified and removed duplicate entries to ensure each transaction was represented only once within the dataset.

5. **Handled Outliers:** Identified and removed unrealistic or extreme values that could distort the results of the analysis and negatively impact business insights.

6. **Corrected Data Inconsistencies:** Reviewed the dataset for spelling mistakes, inconsistent naming conventions, and formatting errors, then standardized these values to improve data integrity.

7. **Prepared the Dataset for Analysis:** After completing the cleaning and validation process, the final dataset was imported into PostgreSQL, where exploratory data analysis was performed using SQL to generate meaningful business insights.



