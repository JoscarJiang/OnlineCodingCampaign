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
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        if (nums1.size() > nums2.size()) {
            swap(nums1, nums2);
        }
        
        int m = nums1.size();
        int n = nums2.size();
        int left = 0, right = m, half_len = (m + n + 1) / 2;
        
        while (left <= right) {
            int partition1 = (left + right) / 2;
            int partition2 = half_len - partition1;
            
            int max_left1 = (partition1 == 0) ? INT_MIN : nums1[partition1 - 1];
            int min_right1 = (partition1 == m) ? INT_MAX : nums1[partition1];
            
            int max_left2 = (partition2 == 0) ? INT_MIN : nums2[partition2 - 1];
            int min_right2 = (partition2 == n) ? INT_MAX : nums2[partition2];
            
            if (max_left1 <= min_right2 && max_left2 <= min_right1) {
                if ((m + n) % 2 == 0) {
                    return (max(max_left1, max_left2) + min(min_right1, min_right2)) / 2.0;
                } else {
                    return max(max_left1, max_left2);
                }
            } else if (max_left1 > min_right2) {
                right = partition1 - 1;
            } else {
                left = partition1 + 1;
            }
        }
        
        // This should never be reached if the input arrays are sorted correctly.
        throw invalid_argument("Input arrays are not sorted.");
    }
};
 ```       

### Analysis

like pivot??
Cannot loop all.

