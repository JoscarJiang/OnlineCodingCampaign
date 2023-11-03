# 2 valid-parentheses From Grind 75 (easy)
**Leetcode Link:** https://leetcode.com/problems/valid-parentheses/description/

**FROM Grind 75 Questions** https://www.techinterviewhandbook.org/grind75

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

- Open brackets must be closed by the same type of brackets.
- Open brackets must be closed in the correct order.
- Every close bracket has a corresponding open bracket of the same type.
 

Example:

"()" -> true   ,     "()[]{}" -> true     ,    "(]" -> false


### Code
```python

class Solution(object):
    def isValid(self, s):
        stack = [] # create an empty stack to store opening brackets
        for c in s: # loop through each character in the string
            if c in '([{': # if the character is an opening bracket
                stack.append(c) # push it onto the stack
            else: # if the character is a closing bracket
                if not stack or \
                    (c == ')' and stack[-1] != '(') or \
                    (c == '}' and stack[-1] != '{') or \
                    (c == ']' and stack[-1] != '['):
                    return False # the string is not valid, so return false
                stack.pop() # otherwise, pop the opening bracket from the stack
        return not stack # if the stack is empty, all opening brackets have been matched with their corresponding closing brackets,
                         # so the string is valid, otherwise, there are unmatched opening brackets, so return false

```

### Analysis
Approach: 
- Using Stack to check every element in the string. 
- If the element is an opening bracket, put it into stack. 
- If the element is a closing bracket and there is an opening bracket before it, match it with the previous bracket. If not matching, return false. If match, pop out the element in stack.


Time complexity: O(n) - traverse the string once and perform constant time operations for each character.

Space complexity:O(n) - the worst-case scenario is when all opening brackets are present in the string and the stack will have to store them all.


**Company Coding Questions:**
https://platform.stratascratch.com/coding?order_field=-attempts_count&code_type=3&job_positions=1&job_positions=2&job_positions=4
**Blind 75 Solu:**
https://docs.google.com/spreadsheets/d/1A2PaQKcdwO_lwxz9bAnxXnIQayCouZP6d-ENrBz_NXc/edit#gid=0
**Blind 75**
https://neetcode.io/practice
