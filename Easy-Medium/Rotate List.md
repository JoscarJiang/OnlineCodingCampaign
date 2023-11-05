## Rotate List

[61. Rotate List](https://leetcode.com/problems/rotate-list/)

Given the head of a linked list, rotate the list to the right by k places.

Input: head = [1,2,3,4,5], k = 2
Output: [4,5,1,2,3]


## Code
```python

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def rotateRight(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        # find the number of nodes
        n = 0
        node = head
        final_node = head
        while node is not None:
            n += 1
            final_node = node
            node = node.next
        
        # rotate n times -> list becomes the same as the original
        if n == 0:
            return head
        k = k % n

        if k == 0:
            return head

        # new head node is at the n-k th
        head_index = n - k

        # find the node before the new_head
        # because you have to set node.next = None
        node = head
        for i in range(head_index - 1):
            node = node.next
        
        # swap
        new_head = node.next
        node.next = None
        final_node.next = head
        return new_head
```

## Analysis
- Time complexity : O(N)
- Space complexity: O(1)
- Note: The key is to know every n times, the list becomes the same. Next, you just need a loop to find the n-k th node and turn it to head.