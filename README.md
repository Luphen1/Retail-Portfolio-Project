# Retail-Portfolio-Project
Retail Insights

# Retail-Portfolio-Project-

#### Table of Contents
---------------------

-  [Project Overview](#Project_Overview)

-  [Data Source](#Data_Source)

-  [Tools](#Tools)

-  [Data Cleaning/Preparation](#Data_Cleaning/Preparation)

-  [Exploration Data Analysis](#Exploration_Data_Analysis)

-  [Data Analysis](#Data_Analysis)

-  [Results/Findings](#Results/Findings)

-  [Recommendations](#Recommendations)

### Project Overview
The provided dataset is a synthetic dataset which represents sales information for a company, containing 5000 entries with 24 columns. The data encompasses various aspects of sales transactions, including order details, customer information, product details, pricing, and shipping information. Below is a detailed breakdown of each column:

### Data Sources
The primary dataset used for this project was downloaded here [Retail Insights](https://www.kaggle.com/datasets/rajneesh231/retail-insights-a-comprehensive-sales-dataset?rvi=1).
Below is a detailed breakdown of each column descriptions below:

1.	Order No: Unique identifier for each order.
2.	Order Date: Date when the order was placed.
3.	Customer Name: Name of the customer placing the order.
4.	Address: Customer's address (one entry appears to be missing).
5.	City: City where the customer is located.
6.	State: State where the customer is located.
7.	Customer Type: Type of customer (e.g., retail, wholesale).
8.	Account Manager: Name of the account manager handling the order.
9.	Order Priority: Priority level of the order.
10.	Product Name: Name of the product being sold.
11.	Product Category: Category to which the product belongs.
12.	Product Container: Container type for the product.
13.	Ship Mode: Mode of shipping for the order.
14.	Ship Date: Date when the order was shipped.
15.	Cost Price: Cost price of the product.
16.	Retail Price: Retail price at which the product is sold.
17.	Profit Margin: Margin between retail and cost prices.
18.	Order Quantity: Quantity of products ordered.
19.	Sub Total: Subtotal cost of the order.
20.	Discount %: Percentage of discount applied to the order.
21.	Discount $: Dollar amount of the discount.
22.	Order Total: Total cost of the order after applying discounts.
23.	Shipping Cost: Cost associated with shipping the order.
24.	Total: Overall total cost, including product cost, discounts, and shipping.

### Tools
 MySQL - Utilized for improving data integrity, data manipulation and data structure.
 Tableau - Utilized for interpreting and communicating insights through visuals and decision-making.

### Exploration Data Analysis
EDA involved exploring the retail dataset to answer key questions such as:


1.	What was the total number of orders per customer?
2.	What was the total number of customers across the dataset?
3.	What was the number of products across the dataset?
4.	What was the total order cost across the dataset?
5.	What was the total ordered quantity by customers?
6.	Target customers with the highest order quantity and order cost for each year.
7.	Find the total order quantity and cost for each order priority.
8.	How does the account manager's sales vary?
9.	What product containers have the highest order quantity?
10.	Find seasonal trends in order quantity for each year.
11.	Find the geographical pattern of product shipping.
12.	Target twenty products with the highest order quantity and total order cost.
13.	What product category has the highest order quantity?
14.	What is the average order value by customer type?


### Data Cleaning/Preparing
In the initial data preparation, I performed the following tasks below:

1. Data loading and inspection.
2. Handling for missing values.
3. Checking for duplicate values.
4. Convert each column to the right data types and eliminating dollar signs contained in any column.
5. Handling Inconsistent data and typos.

### Exploration Data Analysis
EDA involved exploring the retail dataset to answer key questions such as:


1.	What is the total number of orders?
2.	What is the total number of customers across the dataset?
3.	What is the number of products across the dataset?
4.	What is the total order cost across the dataset?
5.	What is the total ordered quantity by customers?
6.	Target top ten customers with the highest order quantity and order cost.
7.	Find the total order quantity and cost for each order priority.
8.	How does the account manager's sales performances across each year?
9.	What product containers have the highest order quantity?
10.	Find seasonal trends in order quantity for each year.
11.	Find the geographical pattern of product shipping.
12.	Target Twenty products with the highest order quantity and total order cost.
13.	What product category has the highest order quantity?
14.	What is the average order value by customer type?




###  Data Analysis
Below are some interesting codes/features and cleaning I worked with:


```
SELECT * FROM retail_sales.cleaned_retail_sales;

```

```
-- Renaming table
RENAME TABLE  retail_sales.cleaned_retail_sales TO retail;
```

```
-- Checking datatypes
DESCRIBE retail;

```
```
USE retail;

```

```
-- Inspecting data 4999 datasets
SELECT * FROM retail;

```

```
-- -- Removed sql dafault security  to update column  `Order Date` and `Ship Date`
SET sql_safe_updates = 0;

SET sql_safe_updates = 1;

```

```

-- Converting ORDERDATE to '%YYYY-MM-DD%'
UPDATE retail
SET `Order Date` = CASE
WHEN `Order Date` LIKE '%/%' THEN DATE_FORMAT(STR_TO_DATE(`Order Date`, '%m/%d/%Y'),'%Y-%m-%d')
WHEN `Order Date` LIKE '%-%' THEN DATE_FORMAT(STR_TO_DATE(`Order Date`, '%d-%m-%Y'),'%Y-%m-%d')
ELSE NULL
END;

```

```
-- Converting ORDERDATE to '%YYYY-MM-DD%'
UPDATE retail
SET `Ship Date` = CASE
WHEN `Ship Date` LIKE '%/%' THEN DATE_FORMAT(STR_TO_DATE(`Ship Date`, '%m/%d/%Y'),'%Y-%m-%d')
WHEN `Ship Date` LIKE '%-%' THEN DATE_FORMAT(STR_TO_DATE(`Ship Date`, '%d-%m-%Y'),'%Y-%m-%d')
ELSE NULL
END;

```

```

-- Converting column Ship Date to date datatype
ALTER TABLE retail
MODIFY COLUMN `Ship Date` DATE NOT NULL;

```

```
-- Converting column Order Date to date datatype
ALTER TABLE retail
MODIFY COLUMN `Sub Total` DOUBLE NOT NULL;

```

```

-- Converting column Cost Price to double data type
ALTER TABLE retail
MODIFY COLUMN `Cost Price` DOUBLE NOT NULL;

```

```
-- Converting column Discount $ to decimal datatype
ALTER TABLE retail
MODIFY COLUMN `Discount $` DECIMAL(10,2) NOT NULL;

```

```
-- Converting column Discount % to decimal datatype
ALTER TABLE retail
MODIFY COLUMN `Discount %` DECIMAL(10,2) NOT NULL;

```

```
-- Converting column Order total to double datatype
ALTER TABLE retail
MODIFY COLUMN `Order Total` DOUBLE NOT NULL;

```

```
-- Converting column shipping cost to double datatype
ALTER TABLE retail
MODIFY COLUMN `Shipping Cost` DOUBLE NOT NULL;

```

```
-- Converting column Total to double datatype
ALTER TABLE retail
MODIFY COLUMN `Total` DOUBLE NOT NULL;

```

```
-- Converting column Profit to double data type
ALTER TABLE retail
MODIFY COLUMN `Profit Margin` DOUBLE NOT NULL;

```
```
-- Converting column column Reatail Price to double data type
ALTER TABLE retail
MODIFY COLUMN `Retail Price` DOUBLE NOT NULL;

```
```
-- Convert column `Order No` to VARCHAR
ALTER TABLE retail
CHANGE COLUMN `ï»¿Order No`  `Order No` VARCHAR(200) NOT NULL;

```
```
--  Removing '$%' in each included columns below
UPDATE retail
SET `Cost Price`  = REPLACE(`Cost Price`, '$', '')
WHERE `Cost Price` LIKE '$%';

```
```
UPDATE retail
SET `Retail Price`  = REPLACE(`Retail Price`, '$', '')
WHERE `Retail Price` LIKE '$%';

```

```
UPDATE retail
SET `Profit Margin`  = REPLACE(`Profit Margin`, '$', '')
WHERE `Profit Margin` LIKE '$%';

```

```

UPDATE retail
SET `Discount $`  = REPLACE(`Discount $`, '$', '')
WHERE `Discount $` LIKE '$%';

```

```
UPDATE retail
SET `Shipping Cost`  = REPLACE(`Shipping Cost`, '$', '')
WHERE `Shipping Cost` LIKE '$%';

```

```

UPDATE retail
SET `Retail Price`  = REPLACE(`Retail Price`, '$', '')
WHERE `Retail Price` LIKE '$%';

```

```

UPDATE retail
SET `Profit Margin`  = REPLACE(`Profit Margin`, '$', '')
WHERE `Profit Margin` LIKE '$%';

```

```

UPDATE retail
SET `Sub Total` = REPLACE(REPLACE(`Sub Total`, '$', ''), ',', '')
WHERE `Sub Total` LIKE '$%';

```

```
UPDATE retail
SET `Order Total` = REPLACE(REPLACE(`Order Total`, '$', ''), ',', '')
WHERE `Order Total` LIKE  '$%';

```

UPDATE retail
SET Total = REPLACE(REPLACE( Total, '$', ''), ',', '')
WHERE Total LIKE  '$%';

```

```

UPDATE retail
SET `Sub Total` = REPLACE(`Sub Total`,',', '')
WHERE `Sub Total`LIKE '$%';

```

```
UPDATE retail
SET `Discount $`  = REPLACE(`Discount $`, '$', '')
WHERE `Discount $` LIKE '$%';

```
```

UPDATE retail
SET `Order Total`  = REPLACE(`Discount $`, '$', '')
WHERE `Order Total` LIKE '$%';

```

```

UPDATE retail
SET `Shipping Cost`  = REPLACE(`Shipping Cost`, '$', '')
WHERE `Shipping Cost` LIKE '$%';

```

```
UPDATE retail
SET Total  = REPLACE(Total, '$', '')
WHERE Total LIKE '$%';

```
```
UPDATE retail
SET `Discount %` = REPLACE(`Discount %`, '%', '')
WHERE `Discount %` LIKE '%';

```

```
-- Changed Column discount $ to percentage 
UPDATE retail
SET `Discount %` = `Discount %` * 0.01;

```

````


-- Handling null values
SELECT 'Order No' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Order No` = NULL
UNION
SELECT 'Order Date' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Order Date` = NULL
UNION
SELECT 'Customer Name' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Customer Name` = NULL
UNION
SELECT 'Address' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Address` = NULL
UNION
SELECT 'City' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `City` = NULL
UNION
SELECT 'State' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `State` = NULL
UNION
SELECT 'Account Manager' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Account Manager` = NULL
UNION
SELECT 'Customer Type' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Customer Type` = NULL
UNION
SELECT 'Order Priority' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Order Priority` = NULL
UNION
SELECT 'Product Name' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Product Name` = NULL
UNION
SELECT 'Product Category' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Product Category` = NULL
UNION
SELECT 'Product Container' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Product Container` = NULL
UNION
SELECT 'Ship Mode' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Ship Mode` = NULL
UNION
SELECT 'Ship Date' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Ship Date` = NULL
UNION
SELECT 'Cost Price' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Cost Price` = NULL
UNION
SELECT 'Order No' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Retail Price` = NULL
UNION
SELECT 'Retail Price' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Order No` = NULL
UNION
SELECT 'Total' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Total` = NULL
UNION
SELECT 'Shipping Cost' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Shipping Cost` = NULL
UNION
SELECT 'Profit Margin' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Profit Margin` = NULL
UNION
SELECT 'Order Quantity' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Order Quantity` = NULL
UNION
SELECT 'Sub Total' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Sub Total` = NULL
UNION
SELECT 'Discount $' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Discount $` = NULL
UNION
SELECT 'Discount %' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Discount %` = NULL
UNION
SELECT 'Order Total' AS columnname,COUNT(*) AS null_count
FROM retail
WHERE `Order Total` = NULL;



````



-- Checking for duplicate values 
 SELECT * FROM retail
 WHERE `Order No` NOT  IN (
    SELECT MIN(`Order No`)
    FROM retail
    GROUP BY `Order No`, `Order Date`, `Customer Name`, Address, City, State, `Customer Type`, `Account Manager`,
             `Order Priority`, `Product Name`, `Product Category`, `Product Container`, `Ship Mode`, `Ship Date`,
             `Cost Price`, `Retail Price`, `Profit Margin`, `Order Quantity`, `Sub Total`, `Discount %`,
             `Discount $`, `Order Total`, `Shipping Cost`, Total);



### Results/Findings:
The analysis results are summarized as follows:

1.There were 4999 orders across the dataset.
2.There were 787 unique customers across the dataset.
3.A total of 257 unique products were purchased by customers.
4.The total order cost was $3,731,457.
5.The total order quantity was 132,3989.
6.Christina Vanderzanden ordered 51 products with a total cost of $18,610.
Michael Oakman ordered 50 products with a total cost of $26,679.
Cindy Chapman ordered 44 products with a total cost of $11,087.
Dave Hallsten ordered 43 products with a total cost of $36,397.
Christopher Martinez ordered 39 products with a total cost of $24,101.
Philip Brown ordered 38 products with a total cost of $11,102.
Patrick Jones ordered 37 products with a total cost of $26,093.
Saphhira Shifley ordered 36 products with a total cost of $34,376.
Jeremy Pistek ordered 35 products with a total cost of $27,214.
7.Not specified and high order priority tend to have the highest order quantity and total cost in my analysis.
8.Here are the managers’ performances for each year:
•In 2013, Tina Carlton had a total order quantity of 2,931 and Connor Betts had a total order cost of $88,480.
•In 2014, Connor Betts had the highest order quantity of 2,785 and a total order cost of $140,794.
•In 2015, Connor Betts had an order quantity of 3,825 and a total order cost of $124,620.
•In 2016, Tina Carlton had an order quantity of 2,792 while Connor Betts had a total order cost of $65,597, and Nicholas Fernandes had a total order quantity of 308 with a total order cost of $13,843.
9.The small box container had the highest total order quantity of 67,365.
10.Seasonal trends by order are as follows:
•June 2015 had an order quantity of 657.
•October 2014 had a total order quantity of 334.
•August 2015 had an order quantity of 574.
•October 2016 had an order quantity of 462.
•January 2017 had an order quantity of 155.
11.The highest order of 9,716 was placed in Sydney [NSW] during the month of December, while the highest order of 4,582 was placed in Melbourne [VIC] during the month of May.
12.I was able to target the top ten products with the highest order quantity and order cost purchased by customers.
13.Consumer customer types tend to have the highest average order quantity of 28.154 per customer type.



 

### Recommendations:

1.Utilize data-driven insights to optimize inventory management, considering the 4,999 orders and 787 unique customers identified across the dataset.
2.Implement targeted marketing strategies to capitalize on the diverse customer base of 787 unique individuals.
3.Focus on promoting the 257 unique products that were purchased by customers to enhance sales and customer satisfaction.
4.Analyze and adjust pricing strategies based on the $3,731,457 total order costs to maximize profitability.
5.Fine-tune supply chain operations to meet the demand reflected in the 132,3989 total order quantities.
6.Recognize top-performing customers like Christina Vanderzanden and Michael Oakman, tailoring special offers to enhance loyalty.
7.Prioritize order specifications and high order priority items to drive increased order quantity and total costs.
8.Monitor managerial performances closely, noting the success of individuals like Connor Betts with consistent high order quantities and total costs.
9.Capitalize on the popularity of items like the small box container, which garnered the highest total order quantity of 67,365.
10.Align marketing campaigns with seasonal trends, targeting peak months such as June 2015 and October 2014 to maximize sales.
11.Identify geographical preferences for ordering, with Sydney and Melbourne exhibiting significant order volume during specific months.
12.Targeting top ten products with the highest order quantities and costs to guide future marketing and inventory decisions. 
13.Offer personalized recommendations and incentives to consumer customers, leveraging their tendency towards higher average order quantities for increased sales.









