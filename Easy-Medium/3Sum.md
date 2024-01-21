## 3Sum


[15. 3Sum](https://leetcode.com/problems/3sum/)

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.


## My Code
It passed but still slow.
```python

numd = {}
        dup = []
        for i in range(len(nums)):
            if nums[i] in numd:
                if len(numd[nums[i]]) <= 2:
                    numd[nums[i]].add(i)
                else:
                    dup.append(i)
            else:
                numd[nums[i]] = {i}
        output = []

        for i in range(len(nums) - 1):
            if i in dup:
                continue
            for j in range(i + 1, len(nums)):
                if j in dup:
                    continue
                s = nums[i] + nums[j]
                if -s in numd:
                    if max(numd[-s]) > j:
                        #sortedns = sorted([nums[i], nums[j], -s])
                        #if sortedns not in output:
                        output.append(tuple(sorted([nums[i], nums[j], -s])))
        output = set(output)
        return output

```

## Better Solution
```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
	res = set()

        #1. Split nums into three lists: negative numbers, positive numbers, and zeros
        n, p, z = [], [], []
        for num in nums:
            if num > 0:
                p.append(num)
            elif num < 0: 
                n.append(num)
            else:
                z.append(num)

        #2. Create a separate set for negatives and positives for O(1) look-up times
        N, P = set(n), set(p)

        #3. If there is at least 1 zero in the list, add all cases where -num exists in N and num exists in P
        #   i.e. (-3, 0, 3) = 0
        if z:
            for num in P:
                if -1*num in N:
                    res.add((-1*num, 0, num))

        #3. If there are at least 3 zeros in the list then also include (0, 0, 0) = 0
        if len(z) >= 3:
            res.add((0,0,0))

        #4. For all pairs of negative numbers (-3, -1), check to see if their complement (4)
        #   exists in the positive number set
        for i in range(len(n)):
            for j in range(i+1,len(n)):
                target = -1*(n[i]+n[j])
                if target in P:
                    res.add(tuple(sorted([n[i],n[j],target])))

        #5. For all pairs of positive numbers (1, 1), check to see if their complement (-2)
        #   exists in the negative number set
        for i in range(len(p)):
            for j in range(i+1,len(p)):
                target = -1*(p[i]+p[j])
                if target in N:
                    res.add(tuple(sorted([p[i],p[j],target])))
        return res


```

## Analysis
- Time complexity : O(N^2)
- Space complexity: O(N)
- Note: My code and better solution are both N^2 of time complexity on avarage, but mine has worse performance when the cases are extreme, like all 0s. Classified discussions can outperform in this case.