# Kultra Mega Stores Inventory Analysis: Case Study 2
by Damilola Olagunju

### Project Overview
The SQL project is Case Study 2 of the end of course project for Data Analysis Course organized by Digital Skillup Academy(DSA).

### Introduction
Kultra Mega Stores (KMS), headquartered in Lagos, specialises in office supplies and furniture. Its customer base includes individual consumers, small businesses (retail), and large corporate clients (wholesale) across Lagos, Nigeria. I was assumed to have been engaged as a Business Intelligence Analyst to support the Abuja division of KMS. The Business Manager has shared an Excel file containing order data from 2009 to 2012 and has requested that I analyze the data, get the answer to some questions and present my key insights and findings.

### Questions/Analysis Tasks
1. Which product category had the highest sales?
2. What are the Top 3 and Bottom 3 regions in terms of sales?
3. What were the total sales of appliances in Ontario?
4. Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers
5. KMS incurred the most shipping cost using which shipping method?
6. Who are the most valuable customers, and what products or services do they typically purchase?
7. Which small business customer had the highest sales?
8. Which Corporate Customer placed the most number of orders in 2009 – 2012?
9. Which consumer customer was the most profitable one?
10. Which customer returned items, and what segment do they belong to?
11. If the delivery truck is the most economical but the slowest shipping method and Express Air is the fastest but the most expensive one, do you think the company appropriately spent shipping costs based on the Order Priority? Explain your answer


### Answers
**1. Which product category had the highest sales?**

```sql
SELECT Product_Category, Sales FROM [dbo].[KMS SQLCASESTUDY2]
WHERE Sales = (SELECT MAX (sales) FROM [dbo].[KMS SQLCASESTUDY2])
```

| Product Category| Total Sale |
|-----------------|------------|
| Technology      |  89061.05  |

**Remark:** 

   ---
   
**2. What are the top 3 and bottom 3 regions in terms of sales?**

Top 3 Regions

```sql
SELECT TOP 3 Region, SUM (Sales) AS total_sales FROM [dbo].[KMS SQLCASESTUDY2]
GROUP BY Region
ORDER BY total_sales DESC

```
| Region  | total sales |
|---------|-------------|
| West    | 3597549.41 |
| Ontario | 3063212.60   |
| Prarie  | 2837304.60    |

  
Bottom 3 Regions

```sql
SELECT TOP 3 Region, SUM (Sales) AS total_sales FROM [dbo].[KMS SQLCASESTUDY2]
GROUP BY Region
ORDER BY total_sales ASC
```
| Region                | Total Sales   |
|-----------------------|---------------|
| Nunavut               |	116376.47    |
| Northwest Territories	|  800847.35    |
| Yukon                 |	975867.39    |

---
  
**3. What were the total sales of appliances in Ontario?**

```sql
SELECT SUM(Sales) AS TotalSales FROM [dbo].[KMS SQLCASESTUDY2]
WHERE Product_Sub_Category = 'Appliances' AND Region = 'Ontario'
```

The total sales for Appliances in Ontario is 202346.84.

---

**4. Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers**


**Comment:** 

---

**5. KMS incurred the most shipping cost using which shipping method?**

```sql
SELECT Ship_Mode, Shipping_Cost FROM [dbo].[KMS SQLCASESTUDY2]
WHERE Shipping_Cost = (SELECT MAX(Shipping_Cost) FROM [dbo].[KMS SQLCASESTUDY2])
```





**6. Who are the most valuable customers, and what products or services do they typically purchase?**
*Assuming that the most valuable customers are the ones that give the company the most profit*

```sql
SELECT top 10 Customer_Name, Product_Name, Profit
FROM [dbo].[KMS SQLCASESTUDY2]
ORDER BY Profit DESC
```

|  |Customer Name	  	   |Product Name	                                                               |   Profit    |
|--|--------------------|-----------------------------------------------------------------------------|-------------|
|1	|Emily Phan	         |Polycom ViewStation™ ISDN Videoconferencing Unit	                           |27220.69     |
|2	|Andy Reiter	      |Polycom ViaVideo™ Desktop Video Communications Unit	                        |14440.39     |
|3	|Deborah Brumfield	|Hewlett Packard LaserJet 3310 Copier	                                       |13340.26     |
|4	|Karen Carlisle	   |Canon Image Class D660 Copier	                                             |12748.86     |
|5	|Rick Wilson	      |Hewlett-Packard Business Color Inkjet 3000 [N, DTN] Series Printers	         |12606.81     |
|6	|Raymond Book        |Hewlett Packard LaserJet 3310 Copier	                                       |11984.40     |
|7	|Logan Haushalter	   |Hewlett Packard LaserJet 3310 Copier	                                       |11630.15     |
|8	|Nick Crebassa	      |Hewlett-Packard Business Color Inkjet 3000 [N, DTN] Series Printers	         |11562.08     |
|9	|John Stevenson	   |Fellowes PB500 Electric Punch Plastic Comb Binding Machine with Manual Bind	|11535.28     |
|10|Grant Carroll	      |Fellowes PB500 Electric Punch Plastic Comb Binding Machine with Manual Bind	|10951.31     |

---

**7. Which small business customer has the highest sales?**

```sql
SELECT TOP 1 Customer_Name, SUM(Sales) as Total_Sales
FROM [dbo].[KMS SQLCASESTUDY2]
WHERE Customer_Segment = 'Small Business'
GROUP BY Customer_Name
ORDER BY Total_Sales DESC
```

|Customer Name	  |Total Sales   |   
|----------------|--------------|
|Dennis Kane	  |75967.59  	  |	

---

**8. Which corporate customer placed the most number of orders in 2009 - 2012?**

```sql
SELECT TOP 1 Customer_Name, COUNT(Order_ID) AS Number_of_Orders
FROM [dbo].[KMS SQLCASESTUDY2]
WHERE Customer_Segment = 'Corporate' 
AND Order_Date >='2009-01-01' 
AND Order_Date <='2012-12-31'
GROUP BY Customer_Name
ORDER BY Number_of_Orders DESC
```

|Customer Name	  |Total Number of Orders |   
|----------------|-----------------------|
|Adam Hart	     |27                     |

---

**9. Which consumer customer was the most profitable one?**

```sql
SELECT top 1 Customer_Name, SUM(Profit) as Total_Profit
FROM [dbo].[KMS SQLCASESTUDY2]
WHERE Customer_Segment = 'Consumer'
GROUP BY Customer_Name
ORDER BY Total_Profit DESC
```

| Customer Name  |Total Profit	|   
|----------------|---------------|
|Emily Phan      |34005.44			|

---

**10. Which customer returned items and what segment do they belong to?**
```sql
SELECT DISTINCT k.Customer_Name, k.Customer_Segment
FROM [dbo].[Order_Status] o
JOIN [dbo].[KMS SQLCASESTUDY2] k
ON o.Order_ID = k.Order_ID
WHERE o.Status = 'Returned'
```

| S/N | Customer Name | Customer Segment |
|-----|---------------|------------------|
| 1 | Aaron Bergman | Corporate |
| 2 | Aaron Hawkins | Home Office |
| 3 | Adam Bellavance | Small Business |
| 4 | Adrian Barton | Small Business |
| 5 | Alan Hwang | Corporate |
| 6 | Alan Hwang | Small Business |
| 7 | Alejandro Grove | Consumer |
| 8 | Alejandro Grove | Corporate |
| 9 | Alejandro Savely | Corporate |
| 10 | Aleksandra Gannaway | Corporate |
| 11 | Alex Russell | Home Office |
| 12 | Alice McCarthy | Corporate |
| 13 | Alyssa Tate | Small Business |
| 14 | Amy Cox | Home Office |
| 15 | Amy Cox | Small Business |
| 16 | Amy Hunt | Home Office |
| 17 | Amy Hunt | Small Business |
| 18 | Anna Chung | Home Office |
| 19 | Anna Gayman | Corporate |
| 20 | Anna Haberlin | Corporate |
| 21 | Anne Pryor | Consumer |
| 22 | Annie Thurman | Consumer |
| 23 | Anthony Garverick | Small Business |
| 24 | Anthony O'Donnell | Consumer |
| 25 | Art Ferguson | Corporate |
| 26 | Art Foster | Home Office |
| 27 | Art Miller | Corporate |
| 28 | Arthur Prichep | Home Office |
| 29 | Arthur Wiediger | Corporate |
| 30 | Ashley Jarboe | Small Business |
| 31 | Astrea Jones | Corporate |
| 32 | Barbara Fisher | Small Business |
| 33 | Barry Blumstein | Small Business |
| 34 | Barry Gonzalez | Small Business |
| 35 | Becky Castell | Consumer |
| 36 | Becky Martin | Home Office |
| 37 | Becky Pak | Corporate |
| 38 | Ben Ferrer | Corporate |
| 39 | Ben Wallace | Home Office |
| 40 | Benjamin Patterson | Corporate |
| 41 | Benjamin Venier | Small Business |
| 42 | Berenike Kampe | Corporate |
| 43 | Beth Thompson | Corporate |
| 44 | Bill Donatelli | Corporate |
| 45 | Bill Donatelli | Small Business |
| 46 | Bill Eplett | Corporate |
| 47 | Bill Overfelt | Corporate |
| 48 | Bill Shonely | Small Business |
| 49 | Bobby Elias | Small Business |
| 50 | Bobby Odegard | Corporate |

---

**11. If the delivery truck is the most economical but the slowest shipping method and Express Air is the fastest**
    **but the most expensive one, do you think the company appropriately spent shipping costs based on the Order Priority?**
    **Explain your answer**



---
