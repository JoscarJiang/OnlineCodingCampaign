## 17 Letter Combinations of a Phone Number
[17 Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number)

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]

### Code
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        results = []
        num_dict = {"2":["a", "b", "c"],
                    "3":["d", "e", "f"],
                    "4":["g", "h", "i"],
                    "5":["j", "k", "l"],
                    "6":["m", "n", "o"],
                    "7":["p", "q", "r", "s"],
                    "8":["t", "u", "v"],
                    "9":["w", "x", "y", "z"]}
        first = True
        for d in digits:
            if first:
                results = num_dict[d]
                first = False
                continue
            results = [r + n for r in results for n in num_dict[d] ]
            
        return results

        
```
### Analysis
- Time complexity : O(N)
- Space complexity: O(3^N)
- Note: easy question.
