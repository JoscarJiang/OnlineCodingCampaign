## Maximum Subarray

[53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray)

Given an integer array nums, find the subarray with the largest sum, and return its sum.

Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: The subarray [4,-1,2,1] has the largest sum 6.


## Code
```python

 def maxSubArray(self, nums: List[int]) -> int:
        m = nums[0]
        s = m if m > 0 else 0
        for num in nums[1:]:
            s = s + num 
            if s < 0:
		# the case [-3, 2] -> max should be 2
                m = max(m, num)
                s = 0
            else:
                m = max(m, s)
        return m

or 

    def maxSubArray(self, nums: List[int]) -> int:
        m = nums[0]
        s = m if m > 0 else 0
        for num in nums[1:]:
            s = s + num 
            if s > m:
                m = s
            if s < 0:
                s = 0
        return m

```

## Analysis
- Time complexity : O(N)
- Space complexity: O(1)
- Note: the key is if the sum of previous array is negative, then drop them