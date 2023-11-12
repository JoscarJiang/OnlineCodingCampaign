## 199 Binary Tree Right Side View
[199 Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view)

Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

Input: root = [1,2,3,null,5,null,4]
Output: [1,3,4]

Input: root = [1,2]
Output: [1,2]

The question is confusing and should be rephrased as **return the values of rightmost node of each layer**. 


### Code
```python

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        stack = []
        rs = []
        node = root
        if node is None:
            return rs
        stack.append(root)
        while len(stack) > 0:
            temp_stack = []
            first = True
            while len(stack) > 0:
                node = stack.pop(0) # pop the first element
                if first:
                    # first element is always the rightmost
                    rs.append(node.val)
                    first = False
                if node.right is not None:
                    temp_stack.append(node.right)
                if node.left is not None:
                    temp_stack.append(node.left)
                
            stack = temp_stack

        return rs
        
```
### Analysis
- Time complexity : O(N)
- Space complexity: O(N)
- Note: use data structure queue. FIFO
