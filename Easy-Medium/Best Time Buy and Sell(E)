# 4 Best time to buy and sell from Grind 75 (easy)
**Leetcode Link:** https://leetcode.com/problems/best-time-to-buy-and-sell-stock

**FROM Grind 75 Questions** https://www.techinterviewhandbook.org/grind75

You are given an array prices where prices[i] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

 

Example 1:

Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.




### Code



#### My Solution(XXX -> exceed the time limit)
```python

class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        profit = 0
        max = 0
        for i in range(len(prices)):
            for j in range(i+1,len(prices)):
                profit = prices[j]-prices[i]
                if profit>0 and profit > max :
                    max = profit
        return max

```

#### Optimized Solution

```python
class Solution(object):
    def maxProfit(self,prices):
        left = 0 #Buy
        right = 1 #Sell
        max_profit = 0
        while right < len(prices):
            currentProfit = prices[right] - prices[left] #our current Profit
            if prices[left] < prices[right]:
                max_profit =max(currentProfit,max_profit)
            else:
                left = right
            right += 1
        return max_profit
 ```       

### Analysis
Cannot loop all.

