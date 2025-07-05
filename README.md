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
1. Which product category had the highest sales?

```sql
SELECT Product_Category, Sales FROM [dbo].[KMS SQLCASESTUDY2]
WHERE Sales = (SELECT MAX (sales) FROM [dbo].[KMS SQLCASESTUDY2])
```

| Product Category| Total Sale |
|-----------------|------------|
| Technology      |  89061.05  |

**Remark:** 

   ---
   
2. What are the top 3 and bottom 3 regions in terms of sales?

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
| Region | Total Sales |
|---------|--------------|
| Nunavut |	116376.47|
| Northwest Territories	| 800847.35|
| Yukon |	975867.39|

---
  
3. What were the total sales of appliances in Ontario?

```sql
SELECT SUM(Sales) AS TotalSales FROM [dbo].[KMS SQLCASESTUDY2]
WHERE Product_Sub_Category = 'Appliances' AND Region = 'Ontario'
```

The total sales for Appliances in Ontario was 202346.84.

---

4. Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers

```sql

```

| product | total sales |
|---------|--------------|
| oodfdf  | 22222       |

6. KMS incurred the most shipping cost using which shipping method?

```sql

```

| product | total sales |
|---------|--------------|
| oodfdf  | 22222       |

7. Who are the most valuable customers, and what products or services do they typically
purchase?

```sql

```

| product | total sales |
|---------|--------------|
| oodfdf  | 22222       |


8. Which small business customer had the highest sales?

```sql

```

| product | total sales |
|---------|--------------|
| oodfdf  | 22222       |


9. Which Corporate Customer placed the most number of orders in 2009 – 2012?

```sql

```

| product | total sales |
|---------|--------------|
| oodfdf  | 22222       |

10. Which consumer customer was the most profitable one?

```sql

```

| product | total sales |
|---------|--------------|
| oodfdf  | 22222       |

11. Which customer returned items, and what segment do they belong to?

```sql

```

| product | total sales |
|---------|--------------|
| oodfdf  | 22222       |

12. If the delivery truck is the most economical but the slowest shipping method and
Express Air is the fastest but the most expensive one, do you think the company
appropriately spent shipping costs based on the Order Priority? Explain your answer

```sql

```

| product | total sales |
|---------|--------------|
| oodfdf  | 22222       |

Other observations and recommendations

Challenges/Limitations
