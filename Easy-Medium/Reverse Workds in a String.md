## Reverse Words in a String

[151. Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string)

A word is defined as a sequence of non-space characters. The words in s will be separated by at least one space.

Return a string of the words in reverse order concatenated by a single space.

Note that s may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

Input: s = "the sky is blue"
Output: "blue is sky the"


## Code
```python
class Solution:
    def reverseWords(self, s: str) -> str:
        words = s.strip().split()
        return " ".join(words[::-1])
```

## Analysis
- Time complexity : O(N)
- Space complexity: O(N)
- Note: Easy question.