## Product of Array Except Self

[238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/description)

Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using the division operation.
Input: nums = [1,2,3,4]
Output: [24,12,8,6]

## Code
```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
	left = [1]
        for num in nums:
            left.append(left[-1] * num)
        left = left[:-1]
        right = [1]
        for i in range(len(nums)-1, -1, -1):
            right.append(right[-1] * nums[i])
        right = right[:-1][::-1]
        return [left[i]* right[i] for i in range(len(left))]
```

## Optimal
```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
	n = len(nums)
        left = [1]
        for num in nums:
            left.append(left[-1] * num)
        left = left[:-1]
        right_product = 1
        for i in range(n-1, -1, -1):
            left[i] *= right_product
            right_product = right_product * nums[i]
            
        return left
```

## Analysis
- Time complexity : O(N)
- Space complexity: O(N)
- Note: To find an algorithms with O(n) and without division is tricky. You have to make use of 