
# Dashboard-on-Atliq-Hardware-Company
## Problem Statement
AtliQ Hardware is a company which supplies computer hardware and peripherals to many of clients such as Excel stores, Surge stories across India. AtliQ Hardware head office is situated in Delhi, India and they have many regional office throughout the India.

Market is growing dynamically and Sales Director is facing issue in terms of tracking the Sales in this dynamically growth market and he is having issues with growth of his business, as overall sales was declining. He has regional managers for North India, South and Central India. Whenever he wants to get insight of these region he would call these people and on the phone regional manager give some insights to him.

## Project planning with AIMS Grid
AIMS Grid is a project management tool and it has four component:-

Purpose:

The goal is to make previously hidden sales insights available to the sales team for decision assistance and to automate them to cut down on human data collection time.

Stakeholders:

Those who will be involved in this project as stakeholders include the sales director, the marketing team, the customer support team, the data analytics team, and IT.

End result:

A computerised dashboard that offers immediate and current sales insights to help data-driven decision making.

Success Criteria:

- Dashboard revealing insights on sales orders using the most recent data available

- The sales staff may demonstrate a 10% reduction in costs by making smarter decisions.

- Sales analysts quit manually collecting data in order to reinvest 20% of their business time in value-added activities.

## Data Exploration Using MySQL

MySQL →Servers →Data Import

Show all customer records

`SELECT * FROM sales.customers;`

Show total number of customers

`SELECT count(*) FROM sales.customers;`

Show transactions for Chennai market (market code for chennai is Mark001)

`SELECT * FROM sales.transactions where market_code='Mark001';`

Show distrinct product codes that were sold in chennai

`SELECT distinct product_code FROM sales.transactions where market_code='Mark001';`

Show transactions where currency is US dollars

`SELECT * from sales.transactions where currency="USD";`

Show transactions in 2020 join by date table

`SELECT sales.transactions.*, sales.date.* FROM sales.transactions INNER JOIN sales.date ON transactions.order_date=date.date where date.year=2020;`

Show total revenue in year 2020 in Chennai

`SELECT SUM(transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON transactions.order_date=date.date where date.year=2020 and transactions.market_code="Mark001";`

## Observation
- Sales Qty is in negative which is invalid and also currency is in USD ,so we need to convert it into INR as in finding insight it will be problematics(total sum of revenue)

- Company is doing Sales in India and also might have done in New York and Paris for 1–2 time , so here we will remove it because right now company is doing business only in India so these data are not useful.

## ETL(Extraction Transfoemation and Loading)
Now we will pull data into Power BI and also do Data Cleaning known as ETL(Extract Transform and Load).
Open tableau -> Databases -> MySQL database

## DATA MODELING
- There will be option update automatically click it (it updated records automatically from MYSQL) or we can use extract on right top corner
- Open the sales database
- Then perform star schema 

We are Extracting data from SQL , Transforming and Loading into tableau

## Data Cleaning
- Sales quantity,amount had negative number so used at leat and range filter to remove it
- Market Code had paris and London so filtered market code and remover mark008, mark009.
- Create calculated field (small down arrow of Sales amount) type this code in it
`IF [CURRENCY] == 'USD' THEN [Sales Amount]*80 ELSE [Sales Amount] END`

