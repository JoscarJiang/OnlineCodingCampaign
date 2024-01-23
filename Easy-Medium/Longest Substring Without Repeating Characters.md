## Longest Substring Without Repeating Characters

[3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters)

Given a string s, find the length of the longest substring without repeating characters.

Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.

## Code
```python

def lengthOfLongestSubstring(self, s: str) -> int:
        if len(s) < 2:
            return len(s)
        count = 0
        maxcount = 0
        sub = ""
        repeat = None
        for i in range(0, len(s) - 1):
            if repeat is not None and s[i] != repeat:
                continue
            for j in range(i, len(s)):
                if s[j] not in sub:
                    count +=1
                    sub += s[j]
                else:
                    maxcount = max(maxcount, count)
                    count = 0
                    if s[j] != sub[0]:
                        repeat = s[j]
                    else:
                        repeat = None
                    sub = ""
                    break
        maxcount = max(maxcount, count)
        return maxcount
        
```
## Better Solution

```python
	start = result = 0
        seen = {}
        for i, letter in enumerate(s):
            if seen.get(letter, -1) >= start:
                start = seen[letter] + 1
            result = max(result, i - start + 1)
            seen[letter] = i
        return result

```

## Analysis
- Time complexity : O(N)
- Space complexity: O(1)
- Note: Use dict to store the last place of each character