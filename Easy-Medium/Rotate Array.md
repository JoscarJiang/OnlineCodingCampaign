## Rotate Array

[189. Rotate Array](https://leetcode.com/problems/rotate-array/description)

Given an integer array nums, rotate the array to the right by k steps, where k is non-negative.

Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]


## Code
```python
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        k = k % n
        if n == 1 or k == 0:
            return
        nums[:] = nums[-k:] + nums[:n-k]
```

## Analysis
- Time complexity : O(N)
- Space complexity: O(1)
- Note: When I use nums = nums[-k:] + nums[:n-k], the print results are always the same. Because like pointer in C, nums = nums[-k:] + nums[:n-k], nums points to a new area(Important!). https://stackoverflow.com/questions/57152755/difference-between-nums-nums-1-and-nums-nums-1