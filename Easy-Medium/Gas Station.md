## Gas Station
[134. Gas Station](https://leetcode.com/problems/gas-station/description/)

There are n gas stations along a circular route, where the amount of gas at the ith station is gas[i].

You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from the ith station to its next (i + 1)th station. You begin the journey with an empty tank at one of the gas stations.

Given two integer arrays gas and cost, return the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return -1. If there exists a solution, it is guaranteed to be unique


## Code: First Version
Idea is to seach a accumulated max value and min value, if max >= min, we find it. and enumerate(left + left) is to test in a circle.

```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        left = [gas[i] - cost[i] for i in range(len(gas))]
        # find the accumulated max
        max_value = left[0]
        min_value = left[0]
        max_start = 0
        max_temp = 0
        min_temp = 0
        for i, value in enumerate(left + left):
            max_temp = max_temp + value
            min_temp = min_temp + value
            if max_temp < 0:
                max_temp = 0
                max_start = (i + 1) % len(left)
            elif max_temp > max_value:
                max_value = max_temp
            if min_temp > 0:
                min_temp = 0
            elif min_temp < min_value:
                min_value = min_temp
        
        if max_value >= abs(min_value):
            return max_start
        else:
            return -1
```

## Optimization
It's already O(N), but we can still optimize it.
Remember it's a **circle** and if there exists a solution, then there is only **one solution**.
1. If sum(left) >= 0 -> always a solution. Because if your accumulated sum of some part is negative, you can alwasy move your start point backward to get the sum >= 0. 
2. Only find the start ponit of last series whose sum >= 0 because if the accumulated sum is negative, then this series must be in the middle.

```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        left = [i - j for i,j in zip(gas, cost)]
        if sum(left) < 0:
            # It's a circle so if sum(left) >= 0, there is always a solution
            return -1

        # find the accumulated max
        max_value = 0
        max_start = 0
        for i, value in enumerate(left):
            max_value = max_value + value
            if max_value < 0:
                max_value = 0
                max_start = i + 1
        return max_start
```

## Analysis
- Time complexity : O(n)
- Space complexity: O(n) [if no left list, then it can be reduced to O(1)]
- Note: Similar to find the largest accumulated sum

