# 30 days of Pandas/SQL
**Leetcode Link:** 

https://leetcode.com/studyplan/30-days-of-pandas/

https://leetcode.com/studyplan/top-sql-50/

Streamlit Instructions: https://www.youtube.com/watch?v=B0MUXtmSpiA

### 1 big-countries

https://leetcode.com/problems/big-countries/description/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python

def big_countries(world: pd.DataFrame) -> pd.DataFrame:
    df = world[(world['area']>= 3000000) | (world['population']>= 25000000) ]
    return df[['name','population','area']]

```
condition 

```sql
select 
name, population,area
from World
where area >= 3000000
or population >= 25000000

```

### 2 recyclable and low fat products
https://leetcode.com/problems/recyclable-and-low-fat-products/description/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata
```python

import pandas as pd

def find_products(products: pd.DataFrame) -> pd.DataFrame:
    df = products[(products['low_fats']=='Y') & (products['recyclable']=='Y')]
    # dataframe [   ['column name']   ]
    return df[['product_id']]

```

```sql

select product_id from Products
where 
low_fats = 'Y'
and
recyclable = 'Y'
```


### 3 Customers who never order
https://leetcode.com/problems/customers-who-never-order/description/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python

def find_customers(customers: pd.DataFrame, orders: pd.DataFrame) -> pd.DataFrame:
    # use ~ to negates the result, do a Complement
    df = customers[~customers['id'].isin(orders['customerId'])]
    df[['Customers']] = df[['name']]
    # or df = df[['name']].rename(columns = {'name': 'Customers'})
    return df[['Customers']]
```
use ~ TO DO COMPLEMENT  
df[ df[''].isin(df['']) ]
df.rename(columns= { 'xx' : 'xx' } )

should also drop_duplicates or unique()

```sql
WITH order_cus AS(
    select distinct customerId from Orders
) 
select distinct name as Customers from customers
where id not in (select customerId from order_cus)
```

### 4 article-views
https://leetcode.com/problems/article-views-i/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python

def article_views(views: pd.DataFrame) -> pd.DataFrame:
    # get the author_id where viewer_id = author_id
    df = views[views['author_id']== views['viewer_id']]
    df = df[['author_id']].rename(columns = {'author_id':'id'})
    # drop duplicate, use df = df[xxx] to make effect like inplace = true
    df.drop_duplicates(subset=['id'],inplace= True)
    # dataframe.sort_values
    df = df.sort_values(by=['id'], ascending = [True])
    return df

```
use dataframe.drop_duplicates(subset= ['']), sort_values(by=[''])

```python
def article_views(views: pd.DataFrame) -> pd.DataFrame:
    authors_viewed_own_articles = views[views['author_id'] == views['viewer_id']]
    unique_authors = authors_viewed_own_articles['author_id'].unique()
    unique_authors = sorted(unique_authors)
    result_df = pd.DataFrame({'id': unique_authors})
    return result_df

```
use dataframe.unique(), sorted(series)

```sql
# Write your MySQL query statement below
select distinct author_id as id
from Views
where viewer_id = author_id
order by id asc
```

### 5 invalid-tweets
https://leetcode.com/problems/invalid-tweets/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata
```python

def invalid_tweets(tweets: pd.DataFrame) -> pd.DataFrame:
    df = tweets[tweets['content'].str.len()>15]
    df_id = df['tweet_id'].unique()
    # cannot return df_id , need to make it a dataframe
    result = pd.DataFrame( {'tweet_id':df_id})
    return result

```
xx_array = df[''].unique()
dff = pd.DataFrame({'' : xx_array })

```sql

select 
distinct tweet_id
from Tweets
where length(content)>15

```
use length in Mysql
len() in sql server


### 6 calculate-special-bonus
https://leetcode.com/problems/calculate-special-bonus/description/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python
def calculate_special_bonus(employees: pd.DataFrame) -> pd.DataFrame:
    # by default 0
    employees['bonus'] = 0
    # dataframe.loc[]
    employees.loc[(employees['employee_id']% 2 !=0) & (~employees['name'].str.startswith('M')),'bonus' ]  = employees['salary']
    df = employees[['employee_id','bonus']].sort_values(by='employee_id', ascending=True)
    return df

```

dataframe.loc[]

dataframe.loc['column'], dataframe.loc[df['shield'] > 6]

df[''].str.startswith()

https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.loc.html

```sql
select 
    employee_id,
    case when employee_id%2<>0 and name not like 'M%' then salary
    else 0
    end as bonus
from Employees
order by employee_id


# or use if

select employee_id, if(employee_id%2!=0 and name not like 'M%',salary,0) as bonus
from Employees
order by employee_id

# orrr use ture-1 false-0

    select employee_id , salary * ( employee_id%2 ) * ( name not like 'M%') as bonus
    from employees
    order by employee_id;

```


### 7 fix-names-in-a-table
https://leetcode.com/problems/fix-names-in-a-table/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python
def fix_names(users: pd.DataFrame) -> pd.DataFrame:
    # str.capitalize() to make name from 'aLice' to 'Alice'
    users['name'] = users['name'].str.capitalize()
    df = users.sort_values(by = 'user_id')

    return df

```
str.capitalize() to make name from 'aLice' to 'Alice'

```sql
SELECT 
  user_id
  ,CONCAT(UPPER(LEFT(name,1)),LOWER(SUBSTRING(name,2))) AS name
FROM Users
ORDER BY user_id
```

use concat(string1, string2)

use UPPER() and LOWER()

LEFT(string, index)

SUBSTRING(string, index)

### 8 find-users-with-valid-e-mails
https://leetcode.com/problems/find-users-with-valid-e-mails/solutions/3853585/regex-explained-pandas-mysql-an-effortless-and-simple-approach-with-comments/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python

def valid_emails(users: pd.DataFrame) -> pd.DataFrame:
    # valid emails, use regex pattern
    users_valid = users[users['mail'].str.match(r'^[A-Za-z][A-Za-z0-9_\.\-]*@leetcode\.com$')]
    return users_valid


```
understand regex
match(r'^  -------   $')

### 9 patients-with-a-condition
https://leetcode.com/problems/patients-with-a-condition/description/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python

def find_patients(patients: pd.DataFrame) -> pd.DataFrame:
    # cannot use this 
    # df = patients[patients['conditions'].str.contains('DIAB1')]


    # The \b in the pattern is a word boundary assertion that ensures 'DIAB1' is a separate word and not part of another word. 
    df = patients[patients['conditions'].str.contains(r'\bDIAB1')]
    return df

```
dd[df[''].str.contains(r'')]

### 10 nth-highest-salary
https://leetcode.com/problems/nth-highest-salary/description/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python
def nth_highest_salary(employee: pd.DataFrame, N: int) -> pd.DataFrame:
    # df is 'IntegerArray' object, has no attribute 'sort_values'
    df = employee['salary'].unique()
    if len(df) < N:
        return pd.DataFrame([np.NaN],columns=[f'getNthHighestSalary({N})'])
    else:
        salary = sorted(df, reverse=True)[N-1]
        # pd.DataFrame([XXXX],columns=[XXX])
        return pd.DataFrame([salary],columns=[f'getNthHighestSalary({N})'])

```

df[].unique()

sorted(IntegerArray)

pd.DataFrame([],columns=[])


### 11 second-highest-salary (M)
https://leetcode.com/problems/second-highest-salary/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python

def second_highest_salary(employee: pd.DataFrame) -> pd.DataFrame:
    salary_arr = employee['salary'].unique()
    # sorted
    salary_ord = sorted(salary_arr, reverse = True)
    if len(salary_ord)>=2:
        ss = salary_ord[1]
        return pd.DataFrame( [ss], columns=['SecondHighestSalary'] )
    else:
        return pd.DataFrame( [np.NaN], columns=['SecondHighestSalary'] ) 

```
array = df[''].unique()
sorted(array)


```python
import pandas as pd

def second_highest_salary(employee: pd.DataFrame) -> pd.DataFrame:
    N=2
    df=employee['salary'].drop_duplicates()
    nf=df.sort_values(ascending=False)
    if N>len(nf):
        return pd.DataFrame({'SecondHighestSalary':[None]})
    n=nf.iloc[N-1]
    return pd.DataFrame({'SecondHighestSalary':[n]})
```

df[''].drop_duplicates
df.sort_values()

### 12 department-highest-salary (M)
https://leetcode.com/problems/department-highest-salary/description/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python

def department_highest_salary(employee: pd.DataFrame, department: pd.DataFrame) -> pd.DataFrame:
    # do a left join
    merge = employee.merge(department.rename(columns={'id':'id_d','name':'name_d'}), left_on = 'departmentId', right_on = 'id_d', how = 'left')
    # do a groupby to find highest salary per depart
    idx = merge.groupby('name_d')['salary'].transform(max) == merge['salary']
    result = merge[idx]
    # cannot use this, only return the first max value for each depart. result = merge.loc[merge.groupby('name_d')['salary'].idxmax()]
    result = result.rename(columns={'name_d':'Department', 'name':'Employee','salary':'Salary'})
    result = result[['Department','Employee','Salary']]
    return result

```
df.merge(df2, left_on='', right_on= '', how='')

df.groupby('')[''].transform(max)

idx  =  df[''] == df[''] -> df[idx]

result[[]]

### 13 rank-scores (M)

https://leetcode.com/problems/rank-scores/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python

def order_scores(scores: pd.DataFrame) -> pd.DataFrame:
    scores = scores.sort_values( by = 'score', ascending = False)
    # use dense method, rank add 1 per group 
    scores['rank'] = scores['score'].rank(method='dense', ascending = False)
    return pd.DataFrame({'score':scores['score'], 'rank': scores['rank']})

```

df[''].rank()


### 14 delete-duplicate-emails

https://leetcode.com/problems/delete-duplicate-emails/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python

def delete_duplicate_emails(person: pd.DataFrame) -> None:
    # order by id
    person.sort_values(by='id', ascending = True, inplace= True)
    # drop duplicates
    person.drop_duplicates(subset='email', keep='first',inplace= True)
 
```
keep an eye on the return

### 15 rearrange-products-table
https://leetcode.com/problems/rearrange-products-table/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python
def rearrange_products_table(products: pd.DataFrame) -> pd.DataFrame:
    # put column into explosion?
    return pd.melt(products,id_vars=['product_id'], var_name='store',value_vars=['store1','store2','store3'], value_name= 'Price').dropna().sort_values(by=['product_id','store'])
    
```
use pd.melt to arrange dataframe
pd.melt(dataframe, id_vars=[''], var_name='', value_vars=[], value_name='')


### 16 count-salary-categories
https://leetcode.com/problems/count-salary-categories/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python
def count_salary_categories(accounts: pd.DataFrame) -> pd.DataFrame:
    low_sal = accounts[accounts['income']<20000]
    avg_sal = accounts[(accounts['income']>=20000) & (accounts['income']<=50000)]
    high_sal = accounts[accounts['income']>50000]

    result = pd.DataFrame({
        'category':['Low Salary','Average Salary','High Salary'],
        'accounts_count':[len(low_sal),len(avg_sal),len(high_sal)]
    })

    fin_result = result.sort_values(by = ['accounts_count'], ascending = False)

    return fin_result

```



```python
def count_salary_categories(accounts: pd.DataFrame) -> pd.DataFrame:
    return pd.DataFrame({
        'category': ['Low Salary', 'Average Salary', 'High Salary'],
        'accounts_count': [
            accounts[accounts.income < 20000].shape[0],
            accounts[(accounts.income >= 20000) & (accounts.income <= 50000)].shape[0],
            accounts[accounts.income > 50000].shape[0],
        ],
    })

```

use df.shape[0] or len(df) to count row number


### 17 find-total-time-spent-by-each-employee
https://leetcode.com/problems/find-total-time-spent-by-each-employee/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata
```python

def total_time(employees: pd.DataFrame) -> pd.DataFrame:
    employees['total_time'] = employees['out_time']-employees['in_time']
    df = employees.groupby(['event_day','emp_id'])['total_time'].agg(sum).reset_index()
    df = df.rename(columns={'event_day':'day'})
    df = df.sort_values(by=['total_time'], ascending = False)
    return df

```
doubke check the df.rename function
don't forget columns={}

use df.groupby([''])[''].agg().reset_index()

### 18 game-play-analysis
https://leetcode.com/problems/game-play-analysis-i/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python

def game_analysis(activity: pd.DataFrame) -> pd.DataFrame:
    # this could not include player_id in the df, only event_date
    # df = activity.groupby(['player_id']).agg({'event_date':min})

    # this could include player_id in the df
    df = activity.groupby(['player_id'])['event_date'].agg('min').reset_index()
    df.rename(columns={'event_date':'first_login'}, inplace=True)
    return df
```

```python
# ORDER
def game_analysis(activity: pd.DataFrame) -> pd.DataFrame:

    df = activity.groupby(['player_id']).agg(
        first_login = ('event_date','min')
    ).reset_index()
    return df

```
df.groupby([])[''].agg()  or **df.groupby(['']).agg({'':''})** or **df.groupby(['']).agg(xxxxxx = ('',''))**
rename(columns={},inplace= True)

### 19 number-of-unique-subjects-taught-by-each-teacher

https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/description/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python
def count_unique_subjects(teacher: pd.DataFrame) -> pd.DataFrame:
    df = teacher.groupby(['teacher_id'])['subject_id'].nunique().reset_index()
    df.rename(columns= {'subject_id':'cnt'},inplace= True)
    return df

```
groupby 

df[''].nunqiue().reset_index()

### 20 classes-more-than-5-students

https://leetcode.com/problems/classes-more-than-5-students/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata
```python

def find_classes(courses: pd.DataFrame) -> pd.DataFrame:
    df = courses.groupby(['class'])['student'].count().reset_index()
    # need to use df[['']] to generate dataframe
    result = df[df['student']>=5][['class']]

    return result

```
need to use df[['']] to generate dataframe

use df[] generate series


### 21 customer-placing-the-largest-number-of-orders

https://leetcode.com/problems/customer-placing-the-largest-number-of-orders/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python

def largest_orders(orders: pd.DataFrame) -> pd.DataFrame:
    df = orders.groupby(['customer_number'])['order_number'].count().reset_index()
    idx = df['order_number'].max() == df['order_number']
    result = df[idx]

    return result[['customer_number']]


```

```python
def largest_orders(orders: pd.DataFrame) -> pd.DataFrame:
    return orders['customer_number'].mode().to_frame()
```

- get max's index(), then get result
- or use mode(). # use to_frame() to Convert Series to DataFrame.


### 22 

https://leetcode.com/problems/group-sold-products-by-the-date/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python
def categorize_products(activities: pd.DataFrame) -> pd.DataFrame:

    # num_sold = activities.groupby(['sell_date','product'])['product'].count()
    # print(num_sold)

    # sell_date   product   
    # 2020-05-30  Basketball    1
    #             Headphone     1
    #             T-Shirt       1
    # 2020-06-01  Bible         1
    #             Pencil        1
    # 2020-06-02  Mask          2

    
    # after counting the number, drop duplicate rows to avoid later product join redundancy
    activities.drop_duplicates(subset=['sell_date','product'],inplace= True)
    # first order by prodcut name, then do the join, to make sure sort products lexicographically
    activities.sort_values(by= ['product'], ascending = True,inplace= True )
    df_num = activities.groupby('sell_date')['product'].count().reset_index()
    df_num.rename(columns={'product': 'num_sold'},inplace= True)
    df = activities.groupby('sell_date', as_index= False).agg(
        {'sell_date':'first', 'product': ','.join}
    )
    df.rename(columns={'product': 'products'},inplace= True)
    result = df_num.merge(df, on ='sell_date' ,how='left')
     # Second order by sell_date
    result.sort_values(by= ['sell_date'], ascending = True )
    return result

```
use two groupby to get num and product lists seperately

use agg({'sell':'first','pp': ','.join}) to get join list

use df.merge(df2, on='',how='')

```python
def categorize_products(activities: pd.DataFrame) -> pd.DataFrame:

    df = activities.groupby('sell_date')['product'].agg(
        [
            ('num_sold', 'nunique'),
            ('products', lambda x : ','.join(sorted(x.unique())))
        ]
    ).reset_index()
    return df

```
use ** xxx.agg([ ('',''),('','') ])**



### 23 daily-leads-and-partners

https://leetcode.com/problems/daily-leads-and-partners/description/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python
def daily_leads_and_partners(daily_sales: pd.DataFrame) -> pd.DataFrame:
    df = daily_sales.groupby(['date_id','make_name']).agg(
        unique_leads =  ('lead_id', 'nunique'),
        unique_partners =  ('partner_id', 'nunique')
    ).reset_index()
    return df

```



### 24 actors-and-directors-who-cooperated-at-least-three-times

https://leetcode.com/problems/actors-and-directors-who-cooperated-at-least-three-times/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python

def actors_and_directors(actor_director: pd.DataFrame) -> pd.DataFrame:
    df = actor_director.groupby(['actor_id','director_id'])['timestamp'].count().reset_index(name='cooperation_count')
    result = df[df['cooperation_count']>=3]
    print(result)
    return result[['actor_id', 'director_id']]


    # df.value_counts()
```
.count().reset_index(name='')



### 25 replace-employee-id-with-the-unique-identifier

https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python

def replace_employee_id(employees: pd.DataFrame, employee_uni: pd.DataFrame) -> pd.DataFrame:
    #merge
    df = employees.merge(employee_uni, on='id',how='left')
    return df[['unique_id','name']]

```

use merge to do the left join

```sql
select 
eu.unique_id as unique_id, e.name as name
from Employees e left join EmployeeUNI eu on e.id = eu.id

```
keep an eye on which table on the left

### 26 students-and-examinations
https://leetcode.com/problems/students-and-examinations/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python

def students_and_examinations(students: pd.DataFrame, subjects: pd.DataFrame, examinations: pd.DataFrame) -> pd.DataFrame:

    df = pd.merge(students, subjects,how='cross')

    count_df = examinations.groupby(['student_id','subject_name']).size().reset_index()
    count_df.rename(columns={0: 'attended_exams' }, inplace = True)

    #####  OR  use xxxx.agg(attended_exams = ('',''))
    # exam_count = examinations.groupby(['student_id', 'subject_name']).agg(
    #     attended_exams=('subject_name', 'count')
    # ).reset_index()

    df2 = df.merge(count_df, on= ['student_id','subject_name'], how='left').fillna(0).sort_values(by=['student_id','subject_name'])

    return df2[['student_id','student_name','subject_name','attended_exams']]
    
    
```
cross merge

groupby value_counts() or size()

reset_index()

fillna(0)



### 27 managers-with-at-least-5-direct-reports

https://leetcode.com/problems/managers-with-at-least-5-direct-reports/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python
def find_managers(employee: pd.DataFrame) -> pd.DataFrame:
    # use as_index=False 'managerId' will be kept as a regular column in the result DataFrame
    df = employee.groupby(['managerId'], as_index= False).agg(
        num = ('id', 'count')
        )

    ##################### 1 ####################
    # result = df[df['num']>=5]
    # return employee[employee['id'].isin(result['managerId'])][['name']]

    ##################### 2 ####################
    # or use how = inner
    result = df[df['num']>=5][['managerId']].merge(employee[['id','name']], left_on='managerId', right_on='id', how='inner')
    return result[['name']]
    
```
employee[employee['id'].isin(result['managerId'])]

merge(xxxxx, how='inner'),
result no null

```sql
with m_5 as (
    select managerId,count(distinct id) as num_e
    from Employee
    group by managerId
    having num_e >=5
)
select name from Employee
where id in (select managerId from m_5)

```
```sql
# beat 84.58%
select a.name
from Employee a
inner join Employee b on a.id = b.managerId
group by a.id
having count(distinct b.id)>=5

```
use inner join
or use cte
if relationship exists


### 28 sales-person
https://leetcode.com/problems/sales-person/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata

```python

def sales_person(sales_person: pd.DataFrame, company: pd.DataFrame, orders: pd.DataFrame) -> pd.DataFrame:

    order_com = orders.merge(company, on='com_id', how='left')
    # get all the sales id related to RED company
    order_com = order_com[order_com['name']== 'RED']
    # use ~ get the complement
    df = sales_person[~sales_person['sales_id'].isin(order_com['sales_id'])][['name']]
    return df

```
use ~ get the complement

### 29 big-countries
https://leetcode.com/problems/big-countries/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata
```python
def big_countries(world: pd.DataFrame) -> pd.DataFrame:
    df = world[
        (world['area']>=3000000) | (world['population'] >=25000000)
    ]
    return df[['name','population','area']]
```

### 30 Confirmation Rate (M)
https://leetcode.com/problems/confirmation-rate/?envType=study-plan-v2&envId=top-sql-50

```python

def confirmation_rate(signups: pd.DataFrame, confirmations: pd.DataFrame) -> pd.DataFrame:

    merged_df = signups.merge(confirmations, on= 'user_id', how='left')
    confirmation_rate_df = (merged_df.groupby('user_id')
                             .agg({'action': lambda x: round((x=='confirmed').mean(),2)})
                             .reset_index()
                             .rename(columns={'action': 'confirmation_rate'}))
    return confirmation_rate_df
```

.agg({'columnxx': lambda x: round((x=='confirmed').mean(),2)})

```sql
# beats 99.00%
# FLOOR() and CEILING() functions to integer
# ROUND() to decimal

with co_num as (
    select 
        user_id,
        count(distinct time_stamp) as total_messages,
        sum(case when action = 'confirmed' then 1 else 0 end) as confirm_num,
        sum(case when action = 'confirmed' then 1 else 0 end)/count(distinct time_stamp) as confirmation_rate
    from Confirmations
    group by user_id
)
select 
    a.user_id,
    case when isnull(b.confirmation_rate) then 0 else round(b.confirmation_rate,2) END as confirmation_rate
from Signups a
left join co_num b on a.user_id = b.user_id

```


```sql
# other solution

select s.user_id, round(avg(if(c.action="confirmed",1,0)),2) as confirmation_rate
from Signups as s left join Confirmations as c on s.user_id= c.user_id group by user_id;

```

round(avg(if(column = 'xxxx',1,0)),2) as dddd
