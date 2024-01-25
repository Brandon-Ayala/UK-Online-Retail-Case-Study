## Data Analysis of a Fictional UK Online Retail Store Using Microsoft Excel and Tableau

### Table of Contents
1. [About This Data](#about)
2. [Ask Phase: What is the Goal?](#ask)
3. [Prepare Phase: Understanding the Data](#prepare)
4. [Process Phase: Cleaning and Organizing the Data](#process)
    * 4.1 [Excel](#excel)
    * 4.2 [Functions used](#functions)
    * 4.3 [Data Limitations](#limitations)
5. [Analyze and Share Phase: What Can We Learn From the Data?](#analyze)
    * 5.1 [Total revenue by year/quarter/month](#analyze1)
    * 5.2 [Top 10 countries by total revenue](#analyze2)
    * 5.3 [Top 10 customers by total revenue](#analyze3)
    * 5.4 [Top 10 products by total revenue](#analyze4)
    * 5.5 [Bottom 10 products by total revenue](#analyze5)
    * 5.6 [20 most returned items](#analyze6)
    * 5.7 [5 countries with highest return percentage](#analyze7)
    * 5.8 [Tableau Dashboard](#tableau)
6. [Act Phase: Conclusions and Recommendations](#act)
    * 6.1 [Recommendations for the store](#act1)
    * 6.2 [Recommendations for future analysis](#act2)

<a id="about"></a>

### 1. About This Data

This dataset represents a year of information for an online retail store based in the UK. There are fields for invoice numbers, stock codes, descriptions of products, quantity of units sold, invoice date and time, unit prices, customer identification numbers, and the customer's country of origin. Invoice numbers can be marked with 'c' to indicate orders that were cancelled.

This data was uploaded to Kaggle.com by user The Devastator and can be found [here.](https://www.kaggle.com/datasets/thedevastator/online-retail-transaction-data/data) The original data comes from [UCI.](https://data.world/uci)

<a id="ask"></a>

### 2. Ask Phase: What is the Goal?

The goals of this analysis are:

1. Identify trends in revenue by quarter, month, country, and customer.
2. Identify the best and worst selling products by revenue offered by the store.
3. Identify which products have the highest return percentage.
4. Identify which countries have the highest return percentage.
5. Create a report on the key findings of this analysis.
6. Create a Tableau dashboard for the store to have access to real-time data.

<a id="prepare"></a>

### 3. Prepare Phase: Understanding the Data

The original dataset comes in the form of one spreadsheet and includes the following information:

* **InvoiceNo:** A 6-digit number uniquely assigned to each transaction. If the number is prefixed by 'c', it indicates a cancellation.
* **StockCode:** A unique identifier for each product sold by the retailer.
* **Description:** The name or a brief description of the product.
* **Quantity:** The number of units of the product sold in each transaction.
* **InvoiceDate:** The date and time when the transaction was made.
* **UnitPrice:** The price per unit of the product in sterling.
* **CustomerID:** A 5-digit number uniquely assigned to each customer.
* **Country:** The country where the customer resides.

<a id="process"></a>

### 4. Process Phase: Cleaning and Organizing the Data

<a id="excel"></a>

#### **Excel**
These are the steps I took to get prepared for this analysis.

* Checked for duplicate entries. None were found.
* Added new column "TotalPrice".
* Added three sheets to calculate return rate percentages. Each sheet has four columns (Description, SalesQuantity, ReturnQuantity, and ReturnPercentage).
    * product_return_percentage
    * country_return_percentage
    * customer_return_percentage
* Created sheet RevenueYrQtrMnthCntryCstmr to house the following pivot tables and charts:
    * Total revenue by year, quarter, and month.
    * Top 10 countries by total revenue.
    * Top 10 customers by total revenue.
* Created sheet TopBottom10Prdct to house the following pivot tables and charts:
    * Top 10 products by total revenue.
    * Bottom 10 products by total revenue.
* Created sheet ReturnPercentagePrdctCntry to house the following pivot tables and charts:
    * 20 most returned items.
    * 5 countries with highest return percentage.

<a id="functions"></a>

#### **Functions Used**

TotalPrice: This function multiplies the Quantity and UnitPrice columns together to create the TotalPrice column.

```=SUM(E2*G2)```

SalesQuantity: This function adds the Quantity together for each product, country, and customer depending on the sheet it's in. It checks if the InvoiceNo column starts with "c". If it starts with "c" then it is a return and it not added to the SalesQuantity.

```=SUMIFS(online_retail!$E$2:$E$541910,online_retail!$D$2:$D$541910,A2,online_retail!$B$2:$B$541910,"<>C*")```

ReturnQuantity: This function does the opposite of the SalesQuantity function. The function checks if the InvoiceNo column starts with "c". If it starts with "c" then it is a return and it is added to the ReturnQuantity.

```=SUMIFS(online_retail!$E$2:$E$541910,online_retail!$D$2:$D$541910,A2,online_retail!$B$2:$B$541910,"C*")```

ReturnPercentage: This function takes the ReturnQuantity, divides it by the SalesQuantity, and then multiplies the result by -100 to make the number a positive percentage of 100. If there are any results that have been divided by zero resulting in a "#DIV/0!" error, it is replaced with "Check" to identify and investigate the results more easily.

```=IFERROR(C2/B2*-100,"Check")```

<a id="limitations"></a>

#### **Data Limitations**

In a real-world scenario I would be asking for clarification on some points:

* There are 135080 records without a CustomerID.
* The Description field has multiple entries with meaningless entries, such as ?, ??, ???.
* The Description field has duplicate entries which mean the same thing, such as ?missing, ??missing, ???missing, and ????missing.
* The Description field has many blank entries.
* There are two entries in the UnitPrice field that have -11062.06 as values to Adjust bad debt.
* There are some items with more returns than units sold. These were removed from visualizations.
* There are some customers with more items returned than items bought. These were removed from visualizations.

<a id="analyze"></a>

### 5. Analyze and Share Phase: What Can We Learn From the Data?

<a id="analyze1"></a>

#### **Total revenue by year/quarter/month**

This pivot table and chart shows the total revenue for all of the data from December 2010 to December 2011 broken down by quarter and month.



Key takeaways: Sales are consistent through the Summer months and start to increase in September. Sales peak in December and are likely to fall in January.

<a id="analyze2"></a>

#### **Top 10 countries by total revenue**

This pivot table and chart shows the top 10 countries by total revenue generated for all of the data.



Key takeaways: United Kingdom is the country taht generates the largest amount of revenue by far. Netherlands, EIRE (Ireland), and Germany comprise of the next three largest countries by revenue.

<a id="analyze3"></a>

#### **Top 10 customers by total revenue**

This pivot table and chart shows the top 10 customers by total revenue generated for all of the data.



Key takeaways: There are a lot of sales without an associated CustomerID. For customers with IDs the top three are 14646, 18102, and 17450. It may be worth reaching out to these customers to determine what new products should be offered.

<a id="analyze4"></a>

#### **Top 10 products by total revenue**

This pivot table and chart shows the top 10 products by total revenue generated for all of the data. There is a filter applied to remove revenue generated from postage.



Key takeaways: The top three products by total revenue generated were the Regency 3 tier cakestand, white hanging heart tealight holder, and party bunting. These are products that should be advertised the most and that the store should have plenty of stock on hand to ensure there are no shortages for orders.

<a id="analyze5"></a>

#### **Bottom 10 products by total revenue**

This pivot table and chart shows the bottom 10 products by total revenue generated for all of the data. There is a filter applied to remove things such as costs for samples, missing or damaged goods, postage, and bank fees.



Key takeaways: All of the items shown in this chart have negative revenue generated. These products should be reevaluated to determine if they are worth offering in the future.

<a id="analyze6"></a>

#### **20 most returned items**

This pivot table and chart shows the top 20 most returned items by quantity for all of the data. There is a filter to remove items that have a return rate of over 100%.



Key takeaways: All of the items shown in this chart have over a 40% rate of return. The process of shipping or manufacturing these products may be leading to damage or defects when they arrive to customers. These products should be reevaluated to determine if they are worth offering in the future or if there can be improvements made to shipping or manufacturing processes to reduce defects and damages. Additional data about why these products are being returned would allow a more detailed analysis.

<a id="analyze7"></a>

#### **5 countries with highest return percentage**

This pivot table and chart shows the top 5 countries with the highest return percentage for all of the data.



Key takeaways: The USA has the largest return percentage by far at nearly 58%. There needs to be an investigation into what is causing such a large return percentage. There may be an issue with shipping causing defects and damages before products arrive to customers. Additional dat about why products are being returned would allow a more detailed analysis.

<a id="tableau"></a>

#### **[Tableau Dashboard](https://public.tableau.com/views/UK-Online-Retail-Dashboard/Main?:language=en-US&:display_count=n&:origin=viz_share_link)**

In Tableau I refined the graphs more and created a dashboard for the store to track their data in real-time. I also included a table chart to show the total quantity of the top 10 items sold by month. This would allow the store to easier see how many of these products to have available to sell.

<a id="act"></a>

### 6. Act Phase: Conclusions and Recommendations

<a id="act1"></a>

#### Recommendations for the store

* Develop new products or advertise existing products to reduce seasonality of the online store. Currently sales peak in winter months and appear to reduce in spring months.

* Advertise the products generating the most revenue. Make sure that these items are easy to find on the website. Ensure that there is plenty of stock on hand to prevent supply shortages and shipping delays for customers.

* Reevaluate the products that aren't generating positive revenue. These items likely aren't worth keeping available in the store.

* Investigate the reasons for returns of items with the highest return percentages. Defects, items damaged in shipping, and shipping delays can be detrimental to customer satisfaction.

<a id="act2"></a>

#### Recommendations for future analysis

* Make the CustomerID field mandatory. There are 135,000 records that don't have a CustomerID filled out. To still be able to track information like "Samples" there can be a CustomerID used for these categories.

* Create a new field, ReturnReason. This will allow for more detailed analysis about why products are being returned and remove the need to replace the Description field. This field would be a dropdown list with options such as:
    * Cancellation, Product Never Shipped
    * Defect / Damage
    * Shipping Damage
    * Arrived Late
    * Did Not Perform As Expected
    * Unexpected Size
    * Samples
    * Missing
    * Damages Before Shipping
    * Unknown

* Create a new field, Notes. This will remove the need for replacing the Description field, as well as being able to give more context to anything necessary to individual orders.

* Additional years of data would allow a more detailed analysis. Currently with one year of data it appears that the online store has a seasonal peak of sales in winter, but this could also mean that the store is growing with time. Some numbers, like return rates, can also easily become inflated by one large order being cancelled. 