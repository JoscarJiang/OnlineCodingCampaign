# 8 Binary Search

**Leetcode Link:** [[https://leetcode.com/problems/invert-binary-tree/description/](https://leetcode.com/problems/binary-search/submissions/))
**FROM Grind 75 Questions** https://www.techinterviewhandbook.org/grind75

Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1.

You must write an algorithm with O(log n) runtime complexity.


### Code - My Solution

```python

class Solution(object):
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        left, right = 0, len(nums)-1 
        while left <= right:
            if nums[left] < target:
                left +=1
            elif nums[left] > target:
                return -1
            else:
                return left 

            if nums[right] > target:
                right -=1
            elif nums[right] < target:
                return -1
            else:
                return right
            
        return -1
            
 ```

### Code - Faster Solution

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums)-1
        
        while left<=right:
            mid = (left+right)//2
            if nums[mid]==target:
                return mid
            elif nums[mid]>target:
                right = mid-1
            else:
                left = mid+1
        
        return -1
            
 ```

### Analysis
-- use binary search algorithm ， mid = (left+right)//2

