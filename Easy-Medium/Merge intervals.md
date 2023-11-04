## 56 Merge Intervals
[56 Merge Intervals](https://leetcode.com/problems/merge-intervals)

Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]

### Code
```python

class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        # if there is order
        intervals = sorted(intervals,  key=lambda x: x [0])
        new_itv = []
        count = 0
        for i, value in enumerate(intervals):
            if i == 0:
                new_itv.append(value)
                continue
            if value[0] <= new_itv[count][1]:
                # merge
                new_itv[count] = [min(value[0], new_itv[count][0]),
                                max(value[1], new_itv[count][1])]
            else:
                new_itv.append(value)
                count += 1
        return new_itv
        
```
### Analysis
- Time complexity : O(NlogN) = Sorting: NlogN + Loop: N
- Space complexity: O(N)
- Note: sort first and then just become easy to find the merge condition: compare the end of next interval and head of current interval. if overlap -> merge; else create new interval.

