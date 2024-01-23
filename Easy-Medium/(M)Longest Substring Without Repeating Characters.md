# Longest Substring Without Repeating Characters

**Leetcode Link:** [https://leetcode.com/problems/longest-substring-without-repeating-characters/)


### Code

```python

class Solution(object):
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        char_map = {}
        start = 0
        max_length = 0
        max_start = []
        for i in range(len(s)):
            # If the character is repeated and its index is within the current substring
            if s[i] in char_map and char_map[s[i]] >= start:
                start = char_map[s[i]]+1
                # start from (index +1) again
            char_map[s[i]] = i
            current_length = i+1-start
            if max_length< current_length:
                max_length = current_length
                max_start = [start]
            elif max_length == current_length:
                max_start.append(start)
            
            # max substrings (could be multiple)
            print(s[start:start + max_length ] for start in max_start)

        return max_length
            
            
 ```


### Analysis
This function uses a sliding window approach to iterate through the string. The char_index_map dictionary keeps track of the last index where each character appeared. If a character repeats and its index is within the current substring, the starting index of the substring is updated. The length of the current substring is calculated, and the maximum length is updated accordingly. 

