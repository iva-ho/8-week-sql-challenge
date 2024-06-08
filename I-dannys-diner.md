# Intro

The first case study looks at [Danny's Diner](https://8weeksqlchallenge.com/case-study-1/) data. The business needs to understand the basics about their customers to stay afloat.

The case study was created by Danny Ma.
#8WeekSQLChallenge

# Case Study Questions

Each of the following case study questions can be answered using a single SQL statement:

1. What is the total amount each customer spent at the restaurant?
2. How many days has each customer visited the restaurant?
3. What was the first item from the menu purchased by each customer?
4. What is the most purchased item on the menu and how many times was it purchased by all customers?
5. Which item was the most popular for each customer?
6. Which item was purchased first by the customer after they became a member?
7. Which item was purchased just before the customer became a member?
8. What is the total items and amount spent for each member before they became a member?
9. If each $1 spent equates to 10 points and sushi has a 2x points multiplier - how many points would each customer have?
10. In the first week after a customer joins the program (including their join date) they earn 2x points on all items, not just sushi - how many points do customer A and B have at the end of January?

Bonus Questions: Join all the things, Rank all the things

1. What is the total amount each customer spent at the restaurant?
```
SELECT
  	s.customer_id,
	SUM(m.price) AS total_spend
FROM
	dannys_diner.sales s
	LEFT JOIN dannys_diner.menu m
  	ON m.product_id = s.product_id
GROUP BY
	customer_id;
```	
2. How many days has each customer visited the restaurant?
```
SELECT
  	customer_id,
	COUNT(DISTINCT order_date) AS visits
FROM
	dannys_diner.sales
GROUP BY
	customer_id;
```	
3. What was the first item from the menu purchased by each customer?
```
SELECT
  s.customer_id,
  s.order_date,
  m.product_name
FROM
	dannys_diner.sales s
INNER JOIN (
  SELECT
      s.customer_id,
      MIN(s.order_date) date
  FROM
      dannys_diner.sales s
  GROUP BY
    customer_id
    ) d
ON d.customer_id = s.customer_id AND d.date = s.order_date
LEFT JOIN dannys_diner.menu m ON m.product_id = s.product_id
ORDER BY s.customer_id, m.product_name
```	

	
	
