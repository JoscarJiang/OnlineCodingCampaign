# 4 Binary Tree


**FROM Grind 75 Questions** https://www.techinterviewhandbook.org/grind75

## (1) invert-binary-tree (E)
**Leetcode Link:** [https://leetcode.com/problems/invert-binary-tree/description/)

Given the root of a binary tree, invert the tree, and return its root.

### Code

```python

# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution(object):
    def invertTree(self, root):
        """
        :type root: TreeNode
        :rtype: TreeNode
        """
        if root is None:
            return None
        #invertTree function inverts the binary tree
        # Use invertTree to invert the nodes in the left and right branch
        rightSide = self.invertTree(root.right)
        leftSide = self.invertTree(root.left)
        # swap right and left branch
        root.left=rightSide
        root.right=leftSide
        
        return root 
            
 ```


### Analysis
-- use built-in function invertTree() to invert the tree


## (2) binary-tree-level-order-traversal (M)
**Leetcode Link:** [https://leetcode.com/problems/binary-tree-level-order-traversal/description/)

Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).


### Code

```python

# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if root is None:
            return None

        # https://www.liaoxuefeng.com/wiki/1016959663602400/1017681679479008 deque
        q = deque()
        q.append(root)

        # to store the val list for the whole binary tree
        output_list = []

        while len(q):
            # to store the val list for one layer
            value_list = []
            for i in range(len(q)):
                # pop the first left element from the queue and get its value
                layerNode = q.popleft()
                value_list.append(layerNode.val) 
                # add node in the queue, from left to right
                if layerNode.left:
                    q.append(layerNode.left)
                if layerNode.right:
                    q.append(layerNode.right)
            output_list.append(value_list)

        return output_list 


 ```       

### Analysis

-- use deque type, to append node into the queue and pop element from the queue

-- use node.left, node.right to get the node in the next layer

-- O(n), O(n) for time and space complxicity
