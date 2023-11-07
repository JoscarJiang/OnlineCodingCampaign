## 71 Simplify Path
[71 Simplify Path](https://leetcode.com/problems/simplify-path)

Given a string path, which is an absolute path (starting with a slash '/') to a file or directory in a Unix-style file system, convert it to the simplified canonical path.

In a Unix-style file system, a period '.' refers to the current directory, a double period '..' refers to the directory up a level, and any multiple consecutive slashes (i.e. '//') are treated as a single slash '/'. For this problem, any other format of periods such as '...' are treated as file/directory names.

The canonical path should have the following format:

The path starts with a single slash '/'.
Any two directories are separated by a single slash '/'.
The path does not end with a trailing '/'.
The path only contains the directories on the path from the root directory to the target file or directory (i.e., no period '.' or double period '..')
Return the simplified canonical path.

### Code
```python

class Solution:
    def simplifyPath(self, path: str) -> str:
        p = path.split("/")
        new_path = ""
        skip_count = 0
        for i in range(len(p)-1, 0 ,-1):
            if p[i] == "":
                continue
            if p[i] == ".":
                continue
            if p[i] == "..":
                skip_count += 1
                continue
            if skip_count > 0:
                skip_count -= 1
                continue
            if len(new_path) == 0:
                 new_path = p[i]
            else:
                new_path =  p[i] + "/" + new_path
        
        new_path = "/" + new_path
        return new_path

        
```
### Analysis
- Time complexity : O(Nl)
- Space complexity: O(N)
- Note: use the idea of stack. if "." or "", stay the same; if "..", pop the content.(if N continuous ".."s, pop N times after last "..")
