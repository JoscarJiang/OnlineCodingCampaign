# 4 Best time to buy and sell from Grind 75 (easy)
**Leetcode Link:** https://leetcode.com/problems/median-of-two-sorted-arrays/description/

 
Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.

The overall run time complexity should be O(log (m+n)).

 

Example 1:

Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.


### Code



#### My Solution
```python

# sort algorithm
#https://realpython.com/sorting-algorithms-python/#the-merge-sort-algorithm-in-python  
# median 
# https://brilliant.org/wiki/median-finding-algorithm/

class Solution(object):
    def findMedianSortedArrays(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: float
        """
        num = sorted(nums1+nums2)
        if len(num)%2 == 0:
            a=num[len(num)/2]
            b=num[len(num)/2-1]
            # cannot pass if not use 2.0. if use /2, will generate 3+2 /2 =2
            median = (a+b)/2.0
            print(median)
        else:
            median = num[(len(num)-1)/2]
        return median
        

        # find median

```
cannot pass if not use 2.0. if use /2, will generate 3+2 /2 =2

#### Other Solution

```python
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        n1, n2 = len(nums1), len(nums2)
        if n1 > n2:
            return self.findMedianSortedArrays(nums2, nums1)
        n = n1 + n2
        left = (n1 + n2 + 1) // 2
        low, high = 0, n1
        
        while low <= high:
            mid1 = (low + high) // 2
            mid2 = left - mid1
            
            l1 = float('-inf') if mid1 == 0 else nums1[mid1 - 1]
            l2 = float('-inf') if mid2 == 0 else nums2[mid2 - 1]
            r1 = float('inf') if mid1 == n1 else nums1[mid1]
            r2 = float('inf') if mid2 == n2 else nums2[mid2]
            
            if l1 <= r2 and l2 <= r1:
                if n % 2 == 1:
                    return max(l1, l2)
                else:
                    return (max(l1, l2) + min(r1, r2)) / 2.0
            elif l1 > r2:
                high = mid1 - 1
            else:
                low = mid1 + 1
        return 0.0
 ```       

### Analysis

like pivot??

Time complexity:
O(log(min(n1, n2)))

Space complexity:
O(1)

https://leetcode.com/problems/median-of-two-sorted-arrays/solutions/3284038/simplest-python-solution-with-simplest-explanation-log-m-n/

```python
	class Solution:     
		def findMedianSortedArrays(self, a, b):

			l = len(a) + len(b)

			if l % 2:
				return self.get_median(a, b, l // 2)
			else:
				return (self.get_median(a, b, l // 2) + self.get_median(a, b, l // 2 - 1))  / 2

		def get_median(self, a, b, idx):

			if not a:
				return b[idx]
			if not b:
				return a[idx]

			ai = len(a) // 2
			bi = len(b) // 2
			ma = a[ai]
			mb = b[bi]

			if ma > mb:
				ma, mb = mb, ma
				ai, bi = bi, ai
				a, b = b, a

			max_idx_ma = len(a) // 2 + len(b) // 2

			if max_idx_ma < idx:
				med = self.get_median(a[ai+1:], b, idx - (len(a)//2+1))
			else:
				# max_idx_ma < min_idx_mb (because they are different numbers) 
				# => idx <= max_idx_ma <  min_idx_mb => idx < min_idx_mb
				med = self.get_median(a, b[:bi], idx)

			return med
```
