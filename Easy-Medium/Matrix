## Matrix
[542. 01 Matrix](https://leetcode.com/problems/01-matrix/description/)
Given an m x n binary matrix mat, return the distance of the nearest 0 for each cell.

The distance between two adjacent cells is 1.

## Code
```python 
class Solution:
    def updateMatrix(self, mat: List[List[int]]) -> List[List[int]]:
        m = len(mat)
        n = len(mat[0])
        mat_mask = [[-1] * n for _ in range(m)]

        num_sum = m * n
        num_count = 0

        for i in range(m):
            for j in range(n):
                if mat[i][j] == 0:
                    mat_mask[i][j] = 0
                    num_count += 1
        
        distance = 0
        while num_count < num_sum:
            distance += 1
            for i in range(m):
                for j in range(n):
                    if mat_mask[i][j] == distance -1:
                        if i + 1 < m and mat_mask[i + 1][j] == -1:
                            mat_mask[i + 1][j] = distance
                            num_count += 1
                        if i - 1 >= 0 and mat_mask[i - 1][j] == -1:
                            mat_mask[i - 1][j] = distance
                            num_count += 1
                        if j + 1 < n and mat_mask[i][j+1] == -1:
                            mat_mask[i][j+1] = distance
                            num_count += 1
                        if j - 1 >= 0 and mat_mask[i][j-1] == -1:
                            mat_mask[i][j-1] = distance
                            num_count += 1
        return mat_mask
```

## Analysis
- Time complexity : O(n*m*log(n*m))
- Space complexity: O(n*m) 
- Note: Find 0 -> set neighbors which is -1 to 1. Find 1 set neighbors which is -1 to 2......
