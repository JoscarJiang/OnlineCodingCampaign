# 4 Merge two sorted lists (easy)
**Leetcode Link:** [https://leetcode.com/problems/best-time-to-buy-and-sell-stock](https://leetcode.com/problems/merge-two-sorted-lists/description/)

**FROM Grind 75 Questions** https://www.techinterviewhandbook.org/grind75

You are given the heads of two sorted linked lists list1 and list2.

Merge the two lists into one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

Example:
Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]
 


### Code


#### Optimized Solution

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

# sorting algorithm
class Solution(object):
    def mergeTwoLists(self, list1, list2):
        newHead = dummyHead = ListNode()
        while list1 and list2:
            if list1.val < list2.val:
                dummyHead.next = list1
                list1 = list1.next
            else:
                dummyHead.next = list2
                list2 = list2.next
            dummyHead = dummyHead.next
        
        if list1:
            dummyHead.next = list1
        if list2:
            dummyHead.next = list2
        return newHead.next
            
 ```       

### Analysis
Not familiar with listnode in python.
Instruction: https://leetcode.com/problems/merge-two-sorted-lists/solutions/759870/python3-solution-with-a-detailed-explanation-dummy-explained/



