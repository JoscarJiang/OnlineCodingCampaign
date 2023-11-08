# 30 days of Pandas
**Leetcode Link:** https://leetcode.com/studyplan/30-days-of-pandas/



### 1

https://leetcode.com/problems/big-countries/description/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata
```python

def big_countries(world: pd.DataFrame) -> pd.DataFrame:
    df = world[(world['area']>= 3000000) | (world['population']>= 25000000) ]
    return df[['name','population','area']]

```
### 2
https://leetcode.com/problems/recyclable-and-low-fat-products/description/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata
```python

import pandas as pd

def find_products(products: pd.DataFrame) -> pd.DataFrame:
    df = products[(products['low_fats']=='Y') & (products['recyclable']=='Y')]
    # dataframe [   ['column name']   ]
    return df[['product_id']]

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
use dataframe.unique(), sorted(dataframe)


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

https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.loc.html



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
