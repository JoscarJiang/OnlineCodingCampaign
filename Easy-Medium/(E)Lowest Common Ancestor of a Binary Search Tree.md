# 10 Lowest Common Ancestor of a Binary Search Tree


**Leetcode Link:** [https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

**FROM Grind 75 Questions** https://www.techinterviewhandbook.org/grind75

Given a binary search tree (BST), find the lowest common ancestor (LCA) node of two given nodes in the BST.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”

### Code

```python

# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """

        # root itself
        if (root == p or root== q or not root):
            return root

        # recurssion
        left = self.lowestCommonAncestor(root.left, p, q)
        
        right = self.lowestCommonAncestor(root.right, p, q)

        if left and right:
            return root
        elif left:
            return left
        elif right:
            return right
        
 ```

### Code

```python

# considering BST, that the left subtree of each node contains nodes with smaller values and the right subtree contains nodes with greater values
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        
        while True:
            if root.val > p.val and root.val > q.val:
                root = root.left
            elif root.val < p.val and root.val < q.val:
                root = root.right
            else:
                return root

 ```

