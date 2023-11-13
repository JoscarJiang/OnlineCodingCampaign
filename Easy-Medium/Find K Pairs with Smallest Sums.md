## 373. Find K Pairs with Smallest Sums
[373. Find K Pairs with Smallest Sums](https://leetcode.com/problems/find-k-pairs-with-smallest-sums)

You are given two integer arrays nums1 and nums2 sorted in non-decreasing order and an integer k.

Define a pair (u, v) which consists of one element from the first array and one element from the second array.

Return the k pairs (u1, v1), (u2, v2), ..., (uk, vk) with the smallest sums.
Input: nums1 = [1,7,11], nums2 = [2,4,6], k = 3
Output: [[1,2],[1,4],[1,6]]
Explanation: The first 3 pairs are returned from the sequence: [1,2],[1,4],[1,6],[7,2],[7,4],[11,2],[7,6],[11,4],[11,6]

### Code (Memory Limit Exceeded)
```python
class Solution:
    def kSmallestPairs(self, nums1: List[int], nums2: List[int], k: int) -> List[List[int]]:
        results = [[i,j] for i in nums1 for j in nums2]
        results = sorted(results, key=lambda x: x[0] + x[1])
        return results[:k]

        
```
### Best (heap)

```python
class Solution:
    def kSmallestPairs(self, nums1: List[int], nums2: List[int], k: int) -> List[List[int]]:

	for i in range(min(k, len(nums1))):
            heapq.heappush(heap, (nums1[i] + nums2[0], i, 0))
        result = []
    
        while k > 0 and heap:
            val, i, j = heapq.heappop(heap)
            result.append([nums1[i], nums2[j]])
        
            # Push the next pair from nums2 into the heap
            if j + 1 < len(nums2):
                heapq.heappush(heap, (nums1[i] + nums2[j+1], i, j+1))
        
            k -= 1
    
        return result

```


### Analysis
- Time complexity : O(NlogN)
- Space complexity: O(N^2)
- Note: using a heap is find and extract the smallest element among a collection of elements.Compared to sorting, it's more effecient because we don't care about the order of whole set, only the min in the current set.
