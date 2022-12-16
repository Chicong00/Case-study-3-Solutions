# 🥑 Foodie-Fi: Solutions

💻 Work performed on Azure Data Studio 💻

<details>
<summary>
A. Customer Journey
</summary> 
Based off the 8 sample customers provided in the sample from the subscriptions table, write a brief description about each customer’s onboarding journey.

````sql
select s.*,p.plan_name,p.price
from dbo.subscriptions s 
join dbo.plans p 
on s.plan_id = p.plan_id 
where customer_id in (1,4,6,23,49,58,79,80)
order by customer_id
````
**Steps**
1. Choose 8 random customers and analyze behavior of them
2. Which plan did they use ? Did they upgrade plan after use free trial ?

**Results**
|customer_id|plan_id|start_date|plan_name|price|
|---|---|---|---|---|
|1|0|2020-08-01|trial|0.00|
|1|1|2020-08-08|basic monthly|9.90|

Customer_id 1 started with a trial subscription and continued with a basic monthly subscription in 7 days after sign-up.

|customer_id|plan_id|start_date|plan_name|price|
|---|---|---|---|---|
|4|0|2020-01-17|trial|0.00|
|4|1|2020-01-24|basic monthly|9.90|
|4|4|2020-04-21|churn|NULL|

Customer_id 4 started with a trial subscription and continued with a basic monthly subscription in 7 days after sign-up and has churned in 3 months after that.

|customer_id|plan_id|start_date|plan_name|price|
|---|---|---|---|---|
|6|0|2020-12-23|trial|0.00|
|6|1|2020-12-30|basic monthly|9.90|
|6|4|2020-02-26|churn|NULL|

Customer_id 6 started with a trial subscription and continued with a basic monthly subscription in 7 days after sign-up and has churned in 2 months after that.

|customer_id|plan_id|start_date|plan_name|price|
|---|---|---|---|---|
|23|0|2020-05-13|trial|0.00|
|23|3|2020-05-20|pro annual|199.00|

Customer_id 23 started with a trial subscription and continued with a pro annual subscription in 7 days after sign-up.

|customer_id|plan_id|start_date|plan_name|price|
|---|---|---|---|---|
|49|0|2020-04-24|trial|0.00|
|49|2|2020-05-01|pro monthly|19.90|
|49|3|2020-08-01|pro annual|199.00|

Customer_id 49 started with a trial subscription and continued with a pro monthly subscription in 7 days after sign-up and has upgraded to a pro annual in 3 days after that.

|customer_id|plan_id|start_date|plan_name|price|
|---|---|---|---|---|
|58|0|2020-07-04|trial|0.00|
|58|1|2020-07-11|basic monthly|9.90|
|58|3|2020-09-24|pro annual|199.90|

Customer_id 58 started with a trial subscription and continued with a basic monthly subscription in 7 days after sign-up and has upgrade to a pro annual in 2 months 13 days after that.

|customer_id|plan_id|start_date|plan_name|price|
|---|---|---|---|---|
|79|0|2020-07-30|trial|0.00|
|79|2|2020-08-06|pro monthly|19.90|

Customer_id 79 started with a trial subscription and continued with a pro monthly subscription in 7 days after sign-up.

|customer_id|plan_id|start_date|plan_name|price|
|---|---|---|---|---|
|80|0|2020-09-23|trial|0.00|
|80|2|2020-09-30|pro monthly|19.90|
|80|4|2020-01-17|churn|NULL|

Customer_id 80 started with a trial subscription and continued with a pro monthly subscription in 7 days after sign-up and has churned in 3 months after that.

</details>

<details>
<summary>
B. Data Analysis Questions
</summary>
  
### 1. How many customers has Foodie-Fi ever had?
````sql
select count(distinct(customer_id)) customer_count
from dbo.subscriptions
````
**Result**  
|customer_count|
|---|
|1000|
  
### 2. What is the monthly distribution of trial plan start_date values for our dataset - use the start of the month as the group by value ?
````sql
select 
    MONTH(start_date) month, 
    count(distinct customer_id) trial_subs
from dbo.subscriptions s 
join dbo.plans p  
on s.plan_id = p.plan_id 
where plan_name = 'trial'
group by month(start_date)
````
**Result**
|month|trial_subs|
|---|---|  
|1|88|
|2|68|
|3|94|
|4|81|
|5|88|
|6|79|
|7|89|
|8|88|
|9|87|
|10|79|
|11|75|
|12|84|
  
### 3. What plan start_date values occur after the year 2020 for our dataset? Show the breakdown by count of events for each plan_name ?
  
````sql
with event21 AS
(
  SELECT 
    plan_name,
    count(1) event_count_2021
  from dbo.subscriptions s 
  join dbo.plans p 
  on s.plan_id = p.plan_id
  where year(start_date) >= 2021
  group by plan_name
),
event20 AS
(
  SELECT 
    plan_name,
    count(1) event_count_2020
  from dbo.subscriptions s 
  join dbo.plans p 
  on s.plan_id = p.plan_id
  where year(start_date) < 2021
  group by plan_name
)

select event20.plan_name, event_count_2020, event_count_2021 
from event20 
left join event21 
on event20.plan_name = event21.plan_name
order by event_count_2020 DESC
````
**Result**
|plan_name|event_count_2020|event_count_2021|    
|---|---|---|
|trial|1000|NULL|
|basic monthly|538|8|
|pro monthly|479|60|
|churn|236|71|
|pro annual|195|63| 
                               
### 4. What is the customer count and percentage of customers who have churned rounded to 1 decimal place ?
  
### 5. How many customers have churned straight after their initial free trial - what percentage is this rounded to the nearest whole number ?
  
### 6. What is the number and percentage of customer plans after their initial free trial ?
  
### 7. What is the customer count and percentage breakdown of all 5 plan_name values at 2020-12-31?
  
### 8. How many customers have upgraded to an annual plan in 2020 ?
  
### 9. How many days on average does it take for a customer to an annual plan from the day they join Foodie-Fi ?
  
### 10. Can you further breakdown this average value into 30 day periods (i.e. 0-30 days, 31-60 days etc) ?
  
### 11. How many customers downgraded from a pro monthly to a basic monthly plan in 2020 ?

</details>

<details>
<summary>
C. Challenge Payment Question
</summary>

</details>

<details>
<summary>
D. Outside The Box Questions
</summary>

</details>
