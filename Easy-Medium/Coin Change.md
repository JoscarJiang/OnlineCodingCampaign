## Coin Change

[322. Coin Change](https://leetcode.com/problems/coin-change/description/)

You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.

Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

You may assume that you have an infinite number of each kind of coin.

 

Example 1:

Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1

## Code
```python

class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [0] + ([float('inf')] * amount)
        for i in range(1, amount + 1):
            for c in coins:
                if i >= c:
                    dp[i] = min(dp[i - c] + 1, dp[i])
        return dp[amount] if dp[amount] != float('inf') else -1
        
```

## Analysis
- Time complexity : O(N*M) -> N is the amount, M is the number of coins
- Space complexity: O(N)
- Note:Dynamic programming problem. The idea is that for number N, best solution should be 1 coin plus the best solution of (N-#coin number).

For example: coins= [1,3,5] target = 10
dp[0] = 0
dp[1] = 1 # 1 #1coin
dp[2] = 2 # 2 #1coin
dp[3] = 1 # min(dp( 3-1 ) + 1, dp( 3-3 ) + 1)
dp[4] = 2 # min(dp( 4-1 ) + 1, dp( 4-3 ) + 1)
dp[5] = 1 # min(dp( 5-1 ) + 1, dp( 5-3 ) + 1, dp( 5-5 ) + 1)
dp[6] = 2 # min(dp( 6-1 ) + 1, dp( 6-3 ) + 1, dp( 6-5 ) + 1)
dp[7] = 3 # min(dp( 7-1 ) + 1, dp( 7-3 ) + 1, dp( 7-5 ) + 1)
dp[8] = 2 # min(dp( 8-1 ) + 1, dp( 8-3 ) + 1, dp( 8-5 ) + 1)
dp[9] = 3 # min(dp( 9-1 ) + 1, dp( 9-3 ) + 1, dp( 9-5 ) + 1)
dp[10] = 2 # min(dp( 10-1 ) + 1, dp( 10-3 ) + 1, dp( 10-5 ) + 1)

