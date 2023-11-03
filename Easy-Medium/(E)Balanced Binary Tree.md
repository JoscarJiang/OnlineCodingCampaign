# 11 Balanced Binary Tree

**Leetcode Link:** [https://leetcode.com/problems/balanced-binary-tree/description/)

**FROM Grind 75 Questions** https://www.techinterviewhandbook.org/grind75


Given a binary tree, determine if it is height-balanced.

A height-balanced binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.


### Code

```python

# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    # DFS
    def height(self, node):
        if node is None:
            return 0
        
        # check previous left branch, if there is inbalanced before
        leftH = self.height(node.left)
        if leftH == -1:
            return -1

        # check previous right branch, if there is inbalanced before
        rightH = self.height(node.right)
        if rightH == -1:
            return -1

        # check current layer,  if there is inbalanced now
        if abs(leftH - rightH) > 1:
            return -1
        
        # return the height of this node
        return max(leftH,rightH) +1

    def isBalanced(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        return self.height(root) != -1 
            
 ```


### Analysis
-- time c:  O(n)


### Code - Another sol and video, clear code

```python

# https://www.youtube.com/watch?v=dQp1oSkpyb4

class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        
        # is_balanced, height
        def dfs(root):
            if not root:
                return True, 0
            
            left = dfs(root.left)
            right = dfs(root.right)
            
            return left[0] and right[0] \
                and abs(left[1]-right[1]) <= 1 \
                , 1 + max(left[1], right[1])
        
        return dfs(root)[0]


 ```       


