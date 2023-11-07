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


### 6

```python



```
