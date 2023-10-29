## 55 Jump Game
[Jamp Game](https://leetcode.com/problems/jump-game)

You are given an integer array nums. You are initially positioned at the array's first index, and each element in the array represents your maximum jump length at that position.

Return true if you can reach the last index, or false otherwise.

### Code
```python

class Solution:
    def canJump(self, nums: List[int]) -> bool:
        max_jump_to = 0
        for i, num in enumerate(nums):
            if max_jump_to < i:
                # judge whether they can jump over 0
                return False
            max_jump_to = max(max_jump_to, num + i)
            
        return True
```
### Analysis
- Time complexity : O(n)
- Space complexity: O(1)
- Note: maintain a max reachable distance

## 45 Jump Game II
[Jump Game II](https://leetcode.com/problems/jump-game-ii/)

You are given a 0-indexed array of integers nums of length n. You are initially positioned at nums[0].

Each element nums[i] represents the maximum length of a forward jump from index i. In other words, if you are at nums[i], you can jump to any nums[i + j] where:

- 0 <= j <= nums[i] and
- i + j < n
Return the minimum number of jumps to reach nums[n - 1]. The test cases are generated such that you can reach nums[n - 1].

### Code
```python

class Solution:
    def jump(self, nums: List[int]) -> int:
        reach, count, last = 0, 0, 0
        
        # Loop through the array excluding the last element
        for i in range(len(nums)-1):    
            # Update reach to the maximum between reach and i + nums[i]
            reach = max(reach, i + nums[i])
        
            # If i has reached the last index that can be reached with the current number of jumps
            if i == last:
                # Update last to the new maximum reachable index
                last = reach
                # Increment the number of jumps made so far
                count += 1
        
        # Return the minimum number of jumps required
        return count

```
### Analysis
- Time complexity : O(n)
- Space complexity: O(1)
- Note: greedy approach to find the jump steps from the beginning to stops(last == i).
