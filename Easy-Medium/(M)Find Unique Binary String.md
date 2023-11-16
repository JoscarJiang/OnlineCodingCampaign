# Find Unique Binary String (M)
**Leetcode Link:** https://leetcode.com/problems/find-unique-binary-string/?envType=daily-question&envId=2023-11-16

Given an array of strings nums containing n unique binary strings each of length n, return a binary string of length n that does not appear in nums. If there are multiple answers, you may return any of them.

 

Example 1:

Input: nums = ["01","10"]
Output: "11"
Explanation: "11" does not appear in nums. "00" would also be correct.
Example 2:

Input: nums = ["00","01"]
Output: "11"
Explanation: "11" does not appear in nums. "10" would also be correct.
Example 3:

Input: nums = ["111","011","001"]
Output: "101"
Explanation: "101" does not appear in nums. "000", "010", "100", and "110" would also be correct.


### Code

```python
class Solution(object):
    def findDifferentBinaryString(self, nums):
        """
        :type nums: List[str]
        :rtype: str
        """
        result = ''
        for i in range(len(nums)):
            result += '1' if nums[i][i] == '0' else '0'
        return result 

 ```       

### Analysis

diff from every item
