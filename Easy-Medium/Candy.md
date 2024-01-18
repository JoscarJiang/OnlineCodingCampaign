## 135 Candy
[135. Candy](https://leetcode.com/problems/candy/)

There are n children standing in a line. Each child is assigned a rating value given in the integer array ratings.

You are giving candies to these children subjected to the following requirements:

Each child must have at least one candy.
Children with a higher rating get more candies than their neighbors.
Return the minimum number of candies you need to have to distribute the candies to the children.

Example 1:

Input: ratings = [1,0,2]
Output: 5
Explanation: You can allocate to the first, second and third child with 2, 1, 2 candies respectively.

## Code

```python

class Solution:
    def candy(self, ratings: List[int]) -> int:
        if len(ratings) == 1:
            return 1
        nums = [1] * len(ratings)
	# from left to right
        for r in range(len(ratings)):
            if r ==0:
                continue
            if ratings[r] > ratings[r-1]:
                nums[r] = nums[r-1] + 1
        # from right to left
        for r in range(len(ratings)-1,-1,-1):
            if r == len(ratings)-1:
                continue
            if ratings[r] > ratings[r+1]:
                nums[r] = max(nums[r+1] + 1, nums[r])
        return sum(nums)

 ```
## Analysis
- Time complexity : O(N)
- Space complexity: O(N)
- Note: To solve this kind of problem of getting values based on left and right side. You can think of using 2 loops, one is left to right and left, the other is right to left.(but remember for the second loop, compare the result with the previous one to get the final value "max(nums[r+1] + 1, nums[r])"). 

Question: how to proove it is the minimum number for this problem? 


