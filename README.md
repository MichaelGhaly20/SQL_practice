### Problem1

```
select * from SALES_PRODUCTS;
```

| sales_id | product_id | sales_date | sales_amount |
|----------|------------|------------|--------------|
| S1       | P1         | 2021-11-12 | 100          |
| S1       | P2         | 2021-11-12 | 200          |
| S2       | P3         | 2021-04-10 | 300          |
| S3       | P4         | 2021-05-24 | 600          |
| S4       | P5         | 2020-04-16 | 50           |
| S5       | P6         | 2021-04-10 | 250          |
| S6       | P6         | 2021-05-12 | 30           |

```
select * from donations;
```

| donation_id | donor_id | donation_date | donation_type | donation_amount |
|-------------|----------|---------------|---------------|-----------------|
| D1          | DONOR1   | 2021-11-12    | CC            | 150             |
| D2          | DONOR2   | 2021-10-18    | CASH          | 70              |
| D3          | DONOR3   | 2021-04-10    | DEBIT         | 100             |
| D4          | DONOR4   | 2021-05-24    | CC            | 200             |
| D5          | DONOR5   | 2021-06-25    | CC            | 80              |
| D6          | DONOR6   | 2020-01-25    | CC            | 250             |
| D7          | DONOR7   | 2019-03-16    | CC            | 100             |

```
select * from DONATIONS_PRODUCTS
```

| product_id | donation_id | description | product_date | product_price |
|------------|-------------|-------------|--------------|---------------|
| P1         | D1          | Toys        | 2021-11-12   | 100           |
| P2         | D3          | Clothers    | 2021-03-12   | 200           |
| P3         | D3          | Watches     | 2021-04-10   | 300           |
| P4         | D4          | Shoes       | 2021-08-16   | 600           |
| P5         | D5          | Belt        | 2020-10-12   | 50            |
| P6         | D6          | Chairs      | 2020-10-19   | 400           |
| P7         | D7          | Tables      | 2020-10-16   | 1000          |
| P8         | D7          | Spoons      | 2020-10-16   | 200           |

Qn1: Give a monthly report of sales figures for each product for year 2021
```
select PRODUCT_ID, extract(month from sales_date) as month, sum(SALES_AMOUNT) as sales_amount
from SALES_PRODUCTS
group by PRODUCT_ID, month
order by PRODUCT_ID;
```

QN2 - GIVE LIST OF ALL PRODUCTS DONATED BUT NOT SOLD
```
-- LIST SHOULD INCLUDE PRODUCT 1D, DONATION ID, DESC, DATE OF DONATION, SALES AMOUNT OF PRODUCT
select *
from donations_products
where PRODUCT_ID not in (
    select product_id from sales_products
    )
```

### Problem2

``` select * from USER_TRANSACTIONS;```

| id | user_id | item    | purchase_date | revenue |
|----|---------|---------|---------------|---------|
| 1  | 109     | Banana  | 2021-03-03    | 50      |
| 2  | 139     | Milk    | 2021-03-18    | 70      |
| 3  | 120     | Biscuit | 2021-03-18    | 90      |
| 4  | 108     | Apple   | 2021-03-18    | 100     |
| 5  | 130     | Bread   | 2021-03-28    | 60      |
| 6  | 103     | Banana  | 2021-03-29    | 20      |
| 7  | 122     | Apple   | 2021-03-07    | 10      |
| 8  | 125     | Dates   | 2021-03-13    | 40      |
| 9  | 139     | Raisins | 2021-03-30    | 60      |
| 10 | 141     | Banana  | 2021-03-17    | 80      |
| 11 | 116     | Apple   | 2021-03-31    | 100     |
| 12 | 128     | Pear    | 2021-03-04    | 40      |
| 13 | 146     | Banana  | 2021-03-04    | 90      |
| 14 | 119     | Banana  | 2021-03-28    | 30      |
| 15 | 142     | Banana  | 2021-03-09    | 80      |
| 16 | 122     | Bread   | 2021-03-06    | 20      |
| 17 | 128     | Biscuit | 2021-03-24    | 30      |
| 18 | 112     | Banana  | 2021-03-24    | 60      |
| 19 | 149     | Apple   | 2021-03-29    | 50      |
| 20 | 100     | Banana  | 2021-03-18    | 40      |
| 21 | 130     | Milk    | 2021-03-16    | 30      |
| 22 | 103     | Milk    | 2021-03-31    | 100     |
| 23 | 112     | Banana  | 2021-03-23    | 10      |
| 24 | 102     | Bread   | 2021-03-25    | 60      |
| 25 | 120     | Apple   | 2021-03-21    | 70      |
| 26 | 140     | Banana  | 2021-04-03    | 50      |
| 27 | 139     | Milk    | 2021-04-18    | 70      |
| 28 | 120     | Biscuit | 2021-05-12    | 90      |
| 29 | 108     | Apple   | 2021-05-12    | 100     |
| 30 | 130     | Bread   | 2022-01-28    | 60      |
| 31 | 103     | Banana  | 2022-01-25    | 20      |
| 32 | 122     | Apple   | 2022-02-07    | 10      |
| 33 | 125     | Dates   | 2022-02-14    | 40      |
| 34 | 139     | Raisins | 2022-02-20    | 60      |
| 35 | 141     | Banana  | 2022-02-18    | 80      |
| 36 | 120     | Raisins | 2022-02-18    | 70      |
| 37 | 130     | Apple   | 2022-02-18    | 10      |

Q1 - Find out daily active users - display user_id and purchase_date
```
select purchase_date,
       count(distinct user_id) as num_of_users
from USER_TRANSACTIONS
group by purchase_date
order by purchase_date
```

Q2 - Find out Monthly Active users display user id and Year and month of purchase
```
select extract(year from purchase_date) as yearly,
       to_char(purchase_date,'Month') as monthly,
       count(distinct user_id) as num_of_users
from USER_TRANSACTIONS
group by yearly,monthly
```

### Problem3

```select * from spending;```

| user_id | spend_date | platform | amount |
|---------|------------|----------|--------|
| 1       | 2019-07-01 | mobile   | 100    |
| 1       | 2019-07-01 | desktop  | 100    |
| 2       | 2019-07-01 | mobile   | 100    |
| 2       | 2019-07-02 | mobile   | 100    |
| 3       | 2019-07-01 | desktop  | 100    |
| 3       | 2019-07-02 | desktop  | 100    |

Write an SQL query to find the total number of users and the total amount spent using mobile only, desktop only and both mobile and desktop together for each date.

```
with all_spend as (
    select spend_date, user_id, max(platform) as platform, sum(amount) as amount
    from spending
    group by spend_date, user_id
    having count(distinct (platform)) = 1
    union all
    select spend_date, user_id, 'Both', sum(amount) as amount
    from spending
    group by spend_date, user_id
    having count(distinct (platform)) = 2
)
select spend_date, platform, sum(amount) as total_amount, count(distinct(user_id)) as total_users
from all_spend
group by spend_date, platform
```

### Problem4

```select * from leetcode_orders;```

| order_id | customer_id | order_type |
|----------|-------------|------------|
| 1        | 1           | 0          |
| 2        | 1           | 0          |
| 11       | 2           | 0          |
| 12       | 2           | 1          |
| 21       | 3           | 1          |
| 22       | 3           | 0          |
| 31       | 4           | 1          |
| 32       | 4           | 1          |

Write an SQL query to report all the orders based on the following criteria:
- if a customer has at least one order of type 0, do not report any order of type 1 from that customer.
- Otherwise, report all the orders of the customer.
    
```
with temp as (
    select *,
           min(order_type) over (partition by customer_id ) as min_order_type
    from leetcode_orders
)
select order_id, customer_id, order_type
from temp
where (order_type + min_order_type <> 1)
```

| order_id | customer_id | order_type |
|----------|-------------|------------|
| 1        | 1           | 0          |
| 2        | 1           | 0          |
| 11       | 2           | 0          |
| 22       | 3           | 0          |
| 31       | 4           | 1          |
| 32       | 4           | 1          |


### Problem5

``` select * from leetcode_products;```

| product_id | store_1 | store_2 | store_3 |
|------------|---------|---------|---------|
| 0          | 95      | 100     | 105     |
| 1          | 70      |         | 80      |

 Write an SQL query to rearrange the Products table so that each row has (product_id, store, price). if a product is not available in a store, do not include a row with that product_id and store combination in the result table.

```
with temp as (
    select product_id, 'store1' as store, store_1 as price
    from leetcode_products
    where store_1 is not null
    union
    select product_id, 'store2' as store, store_2 as price
    from leetcode_products
    where store_2 is not null
    union
    select product_id, 'store3' as store, store_3 as price
    from leetcode_products
    where store_3 is not null
)
select * from temp
order by product_id,store
```

| product_id | store  | price |
|------------|--------|-------|
| 0          | store1 | 95    |
| 0          | store2 | 100   |
| 0          | store3 | 105   |
| 1          | store1 | 70    |
| 1          | store3 | 80    |


### Problem6

``` select * from comments_and_translations;```

| id | comment   | translation   |
|----|-----------|---------------|
| 1  | very good |               |
| 2  | good      |               |
| 3  | bad       |               |
| 4  | ordinary  |               |
| 5  | cdcdcdcd  | very bad      |
| 6  | excellent |               |
| 7  | ababab    | not satisfied |
| 8  | satisfied |               |
| 9  | aabbaabb  | extraordinary |
| 10 | ccddccbb  | medium        |

Write an SQL query to display the correct message (meaningful message) from the input comments_and_translation table.

```
select
case when translation is null then comment else translation end as output
from comments_and_translations;

or 

select coalesce (translation, comment) as output
from comments_and_translations;
```

| output        |
|---------------|
| very good     |
| good          |
| bad           |
| ordinary      |
| very bad      |
| excellent     |
| not satisfied |
| satisfied     |
| extraordinary |
| medium        |


### Problem7

write a query to arrive at the Output table as shown in below image. Provide the solution without using subqueries.

![image](https://user-images.githubusercontent.com/59583421/158645663-7efa859f-45a2-474c-91a9-874d84884182.png)


```
select s.id, 'Mismatch' as Comment
from source s
join target t
on t.id = s.id and s.name <> t.name

union

select s.id, 'new in source' as Comment
from source s
left join target t
on t.id = s.id
where t.id is null

union

select t.id, 'new in target' as Comment
from source s
right join target t
on t.id = s.id
where s.id is null;
```


### Problem8

``` select * from teams;```

| team_code | team_name                   |
|-----------|-----------------------------|
| RCB       | Royal Challengers Bangalore |
| MI        | Mumbai Indians              |
| CSK       | Chennai Super Kings         |
| DC        | Delhi Capitals              |
| RR        | Rajasthan Royals            |
| SRH       | Sunrisers Hyderbad          |
| PBKS      | Punjab Kings                |
| KKR       | Kolkata Knight Riders       |
| GT        | Gujarat Titans              |
| LSG       | Lucknow Super Giants        |

write an sql query such that each team play with every other team just once.
Also write another query such that each team plays with every other team twice.

```
with matches as (
    select row_number() over (order by team_name) as ID, team_code, team_name
    from teams t
)
select team.team_name as team, opponent.team_name as oppnent
from matches team
join matches opponent
on team.id < opponent.id;
```

| team                        | oppnent                     |
|-----------------------------|-----------------------------|
| Chennai Super Kings         | Delhi Capitals              |
| Chennai Super Kings         | Gujarat Titans              |
| Chennai Super Kings         | Kolkata Knight Riders       |
| Chennai Super Kings         | Lucknow Super Giants        |
| Chennai Super Kings         | Mumbai Indians              |
| Chennai Super Kings         | Punjab Kings                |
| Chennai Super Kings         | Rajasthan Royals            |
| Chennai Super Kings         | Royal Challengers Bangalore |
| Chennai Super Kings         | Sunrisers Hyderbad          |
| Delhi Capitals              | Gujarat Titans              |
| Delhi Capitals              | Kolkata Knight Riders       |
| Delhi Capitals              | Lucknow Super Giants        |
| Delhi Capitals              | Mumbai Indians              |
| Delhi Capitals              | Punjab Kings                |
| Delhi Capitals              | Rajasthan Royals            |
| Delhi Capitals              | Royal Challengers Bangalore |
| Delhi Capitals              | Sunrisers Hyderbad          |
| Gujarat Titans              | Kolkata Knight Riders       |
| Gujarat Titans              | Lucknow Super Giants        |
| Gujarat Titans              | Mumbai Indians              |
| Gujarat Titans              | Punjab Kings                |
| Gujarat Titans              | Rajasthan Royals            |
| Gujarat Titans              | Royal Challengers Bangalore |
| Gujarat Titans              | Sunrisers Hyderbad          |
| Kolkata Knight Riders       | Lucknow Super Giants        |
| Kolkata Knight Riders       | Mumbai Indians              |
| Kolkata Knight Riders       | Punjab Kings                |
| Kolkata Knight Riders       | Rajasthan Royals            |
| Kolkata Knight Riders       | Royal Challengers Bangalore |
| Kolkata Knight Riders       | Sunrisers Hyderbad          |
| Lucknow Super Giants        | Mumbai Indians              |
| Lucknow Super Giants        | Punjab Kings                |
| Lucknow Super Giants        | Rajasthan Royals            |
| Lucknow Super Giants        | Royal Challengers Bangalore |
| Lucknow Super Giants        | Sunrisers Hyderbad          |
| Mumbai Indians              | Punjab Kings                |
| Mumbai Indians              | Rajasthan Royals            |
| Mumbai Indians              | Royal Challengers Bangalore |
| Mumbai Indians              | Sunrisers Hyderbad          |
| Punjab Kings                | Rajasthan Royals            |
| Punjab Kings                | Royal Challengers Bangalore |
| Punjab Kings                | Sunrisers Hyderbad          |
| Rajasthan Royals            | Royal Challengers Bangalore |
| Rajasthan Royals            | Sunrisers Hyderbad          |
| Royal Challengers Bangalore | Sunrisers Hyderbad          |

![image](https://user-images.githubusercontent.com/59583421/158650826-e20a2a46-93da-4cfa-a4a9-82a2e9ffbeb0.png)


### Case Study


Table 1: Employees

| id | salary |
|----|--------|

Table 2: Projects

| employee_id | project_id | Start_dt | End_dt |
|-------------|------------|----------|--------|

1- Take the 5 lowest paid employees who have done at least 10 projects

    - filter for employees who have done at least 10 projects (HAVING) using end_dt because yuo are asking about `who have done` so the end_dt should be exist
    - order by salary (ORDER BY) -->
    - LIMIT to the 5 lowest

```
SELECT
  e.id
FROM 
  Employees e
INNER JOIN Projects p ON e.id = p.employee_id
GROUP BY e.id
HAVING COUNT(p.end_dt) >= 10
ORDER BY e.salary ASC
LIMIT 5
```

2- What is the sum of the salaries of employees that have not finished a project

    Not finished definitions
    End_dt is NULL
    End_dt is in the future (end_dt > CURRENT_DATE)
    There is no project_id associated with an employee_id in the table 2

```
WITH cte AS 
  (SELECT *, CASE WHEN end_dt is NULL then 1 ELSE 0 END AS null_end_dt FROM Projects)
  
SELECT
  sum(e.salary)
FROM 
  Employees e
INNER JOIN cte p on e.id = p.employee_id
GROUP BY e.id
HAVING COUNT(project_id) = SUM(null_end_dt)

or 

SELECT SUM(salary)
FROM 
  Employees e
WHERE e.id IS NOT IN (
  SELECT employee_id
  FROM Projects
  WHERE end_dt IS NOT NULL
) 
```


### Case Study


``` select * from user_table;```

| id | name  | user_type |
|----|-------|-----------|
| 1  | Matt  | user      |
| 2  | John  | user      |
| 3  | Louis | admin     |

``` select * from traffic_table;```

| user_id | visited_on | time_spent |
|---------|------------|------------|
| 1       | 2019-05-01 | 15         |
| 2       | 2019-05-03 | 10         |
| 2       | 2019-05-02 | 20         |

Write an SQL query to show the **3 day moving average** of time spent on the website for **'user' user_type**. Round the average time spent to 4 decimal places.

![image](https://user-images.githubusercontent.com/59583421/159279426-3c557175-1c3a-4e9d-b27b-d1070d90dfa3.png)

```
with temp as (
    select tt.visited_on, sum(time_spent) as total
    from traffic_table tt
             left join user_table ut
                       on tt.user_id = ut.id
    where ut.user_type = 'user'
    group by tt.visited_on

)
select visited_on,
       avg(total) over(order by visited_on rows between 2 preceding and current row) as day_rolling_avg
from temp;
```


### Problem9


```select * from amazon_users;```

| user_id | name   | join_date  |
|---------|--------|------------|
| 1       | Jon    | 2020-02-14 |
| 2       | Jane   | 2020-02-14 |
| 3       | Jill   | 2020-02-15 |
| 4       | Josh   | 2020-02-15 |
| 5       | Jean   | 2020-02-16 |
| 6       | Justin | 2020-02-17 |
| 7       | Jeremy | 2020-02-18 |

```select * from events;```

| user_id | type  | access_date |
|---------|-------|-------------|
| 1       | Pay   | 2020-03-01  |
| 2       | Music | 2020-03-02  |
| 2       | P     | 2020-03-12  |
| 3       | Music | 2020-03-15  |
| 4       | Music | 2020-03-15  |
| 1       | P     | 2020-03-16  |
| 3       | P     | 2020-03-22  |

Prime subscription rate by product action 
Given the following two tables, return the fraction of users, rounded to two decimal places,
who accessed Amazon music and upgraded to prime membership within the first 30 days of signing up.
10 users => 5 access amazon music => 2 purchases membership => 2/5

```
select --u.*,e.type, e.access_date, e.access_date - u.join_date
count(distinct u.user_id) as total_users,
       count(distinct case when e.access_date - u.join_date < 30 then u.user_id end),
       1.0*count(distinct case when e.access_date - u.join_date < 30 then u.user_id end) / count(distinct u.user_id)
from amazon_users u
Left join events e
on u.user_id = e.user_id and e.type = 'P'
where u.user_id in (select user_id from events where type = 'Music')
```

### Customer retention and customer churn metrics

Customer retention refers to a company's ability to turn customers into repeat buyers
and prevent them from switching to a competitor.
It indicates whether your product and the quality of your service please your existing customers
    reward programs (cc companies)
    wallet cash back (paytm/gpay)
    retention period

```
select * from transactions;
```

| order_id | cust_id | order_date | amount |
|----------|---------|------------|--------|
| 1        | 1       | 2020-01-15 | 150    |
| 2        | 1       | 2020-02-10 | 150    |
| 3        | 2       | 2020-01-16 | 150    |
| 4        | 2       | 2020-02-25 | 150    |
| 5        | 3       | 2020-01-10 | 150    |
| 6        | 3       | 2020-02-20 | 150    |
| 7        | 4       | 2020-01-20 | 150    |
| 8        | 5       | 2020-02-20 | 150    |

Customer retention
```
select extract(month from this_month.order_date) as month_date, count(distinct last_month.cust_id)
from transactions this_month
left join transactions last_month
on
    this_month.cust_id = last_month.cust_id
    and (extract(month from this_month.order_date) - extract(month from last_month.order_date)) = 1
group by
extract(month from this_month.order_date);
```

| month_date | count |
|------------|-------|
| 1          | 0     |
| 2          | 3     |

Customer Churn
```
select extract(month from last_month.order_date) as month_date, count(distinct last_month.cust_id)
from transactions last_month
left join transactions this_month
on
    this_month.cust_id = last_month.cust_id
    and (extract(month from this_month.order_date) - extract(month from last_month.order_date)) = 1
where this_month.cust_id is null
group by
extract(month from last_month.order_date);
```

| month_date | count |
|------------|-------|
| 1          | 1     |
| 2          | 4     |


### Problem10

```
select * from amazon_users;
```

| user_id | name   | join_date  |
|---------|--------|------------|
| 1       | Jon    | 2020-02-14 |
| 2       | Jane   | 2020-02-14 |
| 3       | Jill   | 2020-02-15 |
| 4       | Josh   | 2020-02-15 |
| 5       | Jean   | 2020-02-16 |
| 6       | Justin | 2020-02-17 |
| 7       | Jeremy | 2020-02-18 |

```
select * from events;
```

| user_id | type  | access_date |
|---------|-------|-------------|
| 1       | Pay   | 2020-03-01  |
| 2       | Music | 2020-03-02  |
| 2       | P     | 2020-03-12  |
| 3       | Music | 2020-03-15  |
| 4       | Music | 2020-03-15  |
| 1       | P     | 2020-03-16  |
| 3       | P     | 2020-03-22  |

Prime subscription rate by product action
Given the following two tables, return the fraction of users, rounded to two decimal places,
who accessed Amazon music and upgraded to prime membership within the first 30 days of signing up.
10 users => 5 access amazon music => 2 purchases membership => 2/5

```
select --u.*,e.type, e.access_date, e.access_date - u.join_date
count(distinct u.user_id) as total_users,
       count(distinct case when e.access_date - u.join_date < 30 then u.user_id end),
       1.0*count(distinct case when e.access_date - u.join_date < 30 then u.user_id end) / count(distinct u.user_id)
from amazon_users u
Left join events e
on u.user_id = e.user_id and e.type = 'P'
where u.user_id in (select user_id from events where type = 'Music')
```

| total_users | count | ?column?               |
|-------------|-------|------------------------|
| 3           | 1     | 0.33333333333333333333 |


### Problem11

```
select * from leetcode_UserActivity;
```

| username | activity | startdate  | enddate    |
|----------|----------|------------|------------|
| Alice    | Travel   | 2020-02-12 | 2020-02-20 |
| Alice    | Dancing  | 2020-02-21 | 2020-02-23 |
| Alice    | Travel   | 2020-02-24 | 2020-02-28 |
| Bob      | Travel   | 2020-02-11 | 2020-02-18 |

Get the Second Most Recent Activity, if there is only one activity then retunr that one

```
with temp as (
    select username,
           activity,
           endDate,
           count(1) over (partition by username)                as total_activities,
           rank() over (partition by username order by endDate) as rn
    from leetcode_UserActivity
)
select * from temp
where total_activities = 1 or rn = 2;
```

| username | activity | enddate    | total_activities | rn |
|----------|----------|------------|------------------|----|
| Alice    | Dancing  | 2020-02-23 | 3                | 2  |
| Bob      | Travel   | 2020-02-18 | 1                | 1  |


### Problem12

```
select * from event_status;
```

| event_time | status |
|------------|--------|
| 10:01      | on     |
| 10:02      | on     |
| 10:03      | on     |
| 10:04      | off    |
| 10:07      | on     |
| 10:08      | on     |
| 10:09      | off    |
| 10:11      | on     |
| 10:12      | off    |

```
with t1 as (
select *,lag(status,1,status) over (order by event_time) as prev_status 
from event_status
), 
t2 as (
select *, sum(case when status='on' and prev_status='off' then 1 else 0 end) over (order by event_time)  as group_key
from t1
)
select min(event_time) as login_time,
max(event_time) as logout_time,
count(*)-1 as cnt
from t2
group by group_key
order by login_time
```

| login_time | logout_time | cnt |
|------------|-------------|-----|
| 10:01      | 10:04       | 3   |
| 10:07      | 10:09       | 2   |
| 10:11      | 10:12       | 1   |
