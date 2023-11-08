## 148 Sort List
[148 Sort List](https://leetcode.com/problems/sort-list)

Given the head of a linked list, return the list after sorting it in ascending order.

Input: head = [4,2,1,3]
Output: [1,2,3,4]

### Code
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def sortList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        node = head
        l = []
        while node is not None:
            l.append(node)
            node = node.next
        n = len(l)
        if n <= 1:
            return head
        l = sorted(l, key=lambda x: x.val)
        for i in range(n-1):
            l[i].next = l[i+1]
        l[n-1].next = None
        return l[0]

        
```
### Analysis
- Time complexity : O(NlogN)
- Space complexity: O(N)
- Note: sort first and relink them. What about use O(1) space? QuickSort to change the link.
