# 4 Valid Palindrome (easy)
**Leetcode Link:** https://leetcode.com/problems/valid-palindrome/description/

**FROM Grind 75 Questions** https://www.techinterviewhandbook.org/grind75

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string s, return true if it is a palindrome, or false otherwise.

Example 1:

Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.


### Code



#### My Solution(Beats 91.82%)
```python

import re
class Solution(object):
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        # converting all uppercase letters into lowercase letters
        s = s.lower()
        # removing all non-alphanumeric characters
        s = re.sub(r'[^a-zA-Z0-9]', '', s)
        # test palindrome or not - compare [i] [-()i+1)]
        for i in range(len(s)//2):
            if s[i] != s[-(i+1)]:
                return False
        return True

```

-- use re.sub(r'[^a-zA-Z0-9]','',string)

-- compare the s[i] with s[-(I+1)]

#### Optimized Solution (98%)

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        s1 = ''
        for c in s.lower():
            if c.isalnum():
                s1 += c

        return True if s1==s1[::-1] else False
 ```       
-- use isalnum() function

-- compare s with s[::-1]

-- string[::-1], it generates a reversed copy of the original string.


