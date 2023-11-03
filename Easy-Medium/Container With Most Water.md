## 11. Container With Most Water
[11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

## Description

You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

## Code(Time exceeded)

Eevn with some optimization, but it's still hard to pass some test cases.

```python
max_v = 0
        best_j = len(height) - 1
        temp_j = len(height) - 1
        for i in range(len(height)):
            max_height = height[-1]
            
            if i != 0 and height[i] < height[i - 1]:
                continue
            best_j = temp_j
            if  (i + 1 != len(height)) and (i != 0) and (best_j - i - 1) * min(height[i + 1], height[best_j]) > (best_j - i) * min(height[i], height[best_j]):
                continue

            for j in range(best_j, i, -1):
                if height[j] < max_height:
                    continue
                product = min(height[i], height[j]) * (j-i)
                max_height = height[j]
                if product > max_v:
                    max_v = product
                    temp_j = j

        return max_v

```

## Best 

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:

        # find if choose move ahead, how much it should be
        n = len(height)
        # start from 2 ends
        left = 0
        right = n - 1
        max_v = min(height[left], height[right]) * (n - 1)

        # search for higher to the middle
        while left < right:
            max_temp = min(height[left], height[right]) * (right-left)
            if max_temp > max_v:
                max_v = max_temp
            if height[right] > height[left]:
                left += 1
            else:
                right -= 1

        return max_v


```

## Analysis
- Time complexity : O(N)
- Space complexity: O(1)
- Note: The key is to figure out how to move the pointers. Moving from the shorter line to the next can possibly get the better results.
