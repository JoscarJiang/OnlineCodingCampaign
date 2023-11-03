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

    **Other use cases about [start:stop:step] syntax**
    
```python
# reverse using string[::-1]
original_list = [1, 2, 3, 4, 5]
reversed_list = original_list[::-1]
print(reversed_list)  # Output: [5, 4, 3, 2, 1]

# select every X element string[::X]
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
selected_numbers = numbers[::2]  # This selects every second element
print(selected_numbers)  # Output: [1, 3, 5, 7, 9]

# copy a sequence
original = [10, 20, 30, 40, 50]
copied = original[:]

# truncate a Sequence
values = [1, 2, 3, 4, 5, 6, 7, 8, 9]
truncated = values[2:7:2]  # Start at index 2, end at index 7, step 2
print(truncated)  # Output: [3, 5, 7]



 ```       
    


