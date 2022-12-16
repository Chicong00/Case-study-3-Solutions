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
