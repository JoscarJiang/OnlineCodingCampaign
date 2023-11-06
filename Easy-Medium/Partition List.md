## 86 Partition List
[86 Partition List](https://leetcode.com/problems/partition-list/)

Given the head of a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions
Input: head = [1,4,3,2,5,2], x = 3
Output: [1,2,2,4,3,5]

## Code
```python

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def partition(self, head: Optional[ListNode], x: int) -> Optional[ListNode]:
        new_head = ListNode(0, head)
        node_left = new_head
        node_right_prev = new_head
        node_right = head
        flag = False
        
        while node_right is not None:
            if node_right.val >= x:
                # move right_node forward
                node_right_prev = node_right
                node_right = node_right.next
                flag = True
            elif flag == False:
		# fix bugs if elements < x in the beginning. Move together forward
                node_right_prev = node_right
                node_right = node_right.next
                node_left = node_left.next
            else:
                # insert node_right to the node_left.next
                temp = node_left.next
                node_left.next = node_right
                node_right_prev.next = node_right.next
                node_right.next = temp
                node_right = node_right_prev.next
                node_left = node_left.next
        return new_head.next
        
```
## Second Solution: Better to understand
```python
class Solution:
    def partition(self, head: Optional[ListNode], x: int) -> Optional[ListNode]:
        left_head = ListNode(-101, None)
        right_head = ListNode(-101, None)
        left = left_head
        right = right_head
        
        cur = head

        while cur:
            if cur.val <x:
                left.next = cur
                left = left.next
            else:
                right.next = cur
                right = right.next
            cur = cur.next
        
        left.next = right_head.next
        right.next = None
        return left_head.next

```
## Analysis
- Time complexity : O(N)
- Space complexity: O(1)
- Note: Mine is faster but easy to get lost. The Second solution is to use 2 heads to find the elements in order and connect them in the end.

