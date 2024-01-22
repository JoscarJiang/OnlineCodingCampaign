## Minimum Size Subarray Sum

[209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum)

Given an array of positive integers nums and a positive integer target, return the minimal length of a 
subarray whose sum is greater than or equal to target. If there is no such subarray, return 0 instead.


Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2


## Code
```python

 def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        sumt = nums[0]
        start = 0
        end = 0
        length = len(nums)
        minlen = length
        while start <= end and end < length:
            if nums[end] >= target:
                return 1
            if sumt >= target:
                diff = end - start + 1
                if diff  < minlen:
                    minlen = diff
                sumt = sumt - nums[start]
                start += 1
            else:
                end += 1
                if end < length:
                    sumt += nums[end]
        if minlen == length:
            if start == 0:
                return 0
        return minlen

```

## Analysis
- Time complexity : O(N)
- Space complexity: O(1)
- Note: The key is for each end, we adjust the start position and find the minimum.