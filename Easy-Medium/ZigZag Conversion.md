## Zigzag Conversion

[6. Zigzag Conversion](https://leetcode.com/problems/zigzag-conversion)

The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

P   A   H   N
A P L S I I G
Y   I   R
And then read line by line: "PAHNAPLSIIGYIR"

Write the code that will take a string and make this conversion given a number of rows:

string convert(string s, int numRows);


## Code
```python
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if numRows == 1 or numRows >= len(s):
            return s
        news = ""
        l = len(s)
        for i in range(numRows):
            j = i
            step1 = (numRows - i - 1) * 2 
            step2 = i * 2
            while j < l:
                if i != numRows - 1:
                    news += s[j]
                j = step1 + j
                if i == 0:
                    continue
                elif j < l :
                    news +=s[j]
                j = j + step2
        return news

```

## Analysis
- Time complexity : O(N)
- Space complexity: O(N)
- Note: Turn it to math problem.