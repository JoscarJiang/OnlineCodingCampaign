# 4 Valid Palindrome (easy)
**Leetcode Link:** [https://leetcode.com/problems/valid-palindrome/description/](https://leetcode.com/problems/valid-anagram/submissions/)

**FROM Grind 75 Questions** https://www.techinterviewhandbook.org/grind75

Given two strings s and t, return true if t is an anagram of s, and false otherwise.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

Example 1:

Input: s = "anagram", t = "nagaram"
Output: true


### Code



#### My Solution
```python

class Solution(object):
    def isAnagram(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        # first filter
        if len(s) != len(t):
            return False
        # get the occurance for each letter and compare the dicts for two words
        dict_s = {}
        dict_t = {}
        for i in s:
            dict_s[i] = s.count(i)
        for j in t:
            dict_t[j] = t.count(j)
        if dict_t == dict_s:
            return True
        else:
            return False
```

-- use dictionary to store occurance of each letter

-- compare the occurance

-- time cost high

#### Other Solution 

```python

class Solution(object):
    def isAnagram(self, s, t):
        # In case of different length of thpse two strings...
        if len(s) != len(t):
            return False
        for idx in set(s):
            # Compare s.count(l) and t.count(l) for every index i from 0 to 26...
            # If they are different, return false...
            if s.count(idx) != t.count(idx):
                return False
        return True     # Otherwise, return true...


 ```       
-- also use string.count() to count occurance

