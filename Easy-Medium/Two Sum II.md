## Two Sum II - Input Array Is Sorted

[167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted)

Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let these two numbers be numbers[index1] and numbers[index2] where 1 <= index1 < index2 < numbers.length.

Return the indices of the two numbers, index1 and index2, added by one as an integer array [index1, index2] of length 2.

The tests are generated such that there is exactly one solution. You may not use the same element twice.

Your solution must use **only constant extra space**.
## Code
```python

class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        num1 = 0
        num2 = 0
        last = numbers[0] - 1
        n = len(numbers)
        for i in range(n):
            if numbers[i] == last:
                # accelerate point: sorted -> don't need to check again for the same numbers
                continue
            last = numbers[i]
            for j in range(i + 1, n):
                two_sum =  numbers[i] + numbers[j]
                if two_sum == target:
                    num1 = numbers[i]
                    num2 = numbers[j]
                elif two_sum > target:
                    # accelerated point : sorted -> don't need to check the rest
                    break
        
        num1_index = -1
        num2_index = -1
        for i, number in enumerate(numbers):
            if num2_index > 0:
                # num1_index >=0 and num2_index >=0 but num2_index must be found later than num1_index
                break
            if number == num1 and num1_index == -1:
                num1_index = i + 1
            elif number == num2:
                num2_index = i + 1
        return [num1_index, num2_index]
```

## Best
def twoSum(self, numbers: List[int], target: int) -> List[int]:
        left, right = 0, len(numbers)-1 
        sum  = 0
        while left < right:
            sum = numbers[left] + numbers[right]
            if sum > target:
                right -= 1
            elif sum < target:
                left += 1
            else:
                return left+1, right+1

## Analysis
- Time complexity : O(n) -- Best  O(n^2) -- Mine
- Space complexity: O(1)
- Note: First Version is easy to run long time even with some accelebrating techniques.
Second solution makes use of sorted features, using 2 pointers starting from left and right to find. 
        
