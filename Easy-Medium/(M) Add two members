# Add two members

**Leetcode Link:** [https://leetcode.com/problems/add-two-numbers/submissions/)

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.

(+ calculation)

### Code

```python

# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        # Initialize a dummy head to simplify code
        dummyHead = ListNode(0)
        cur = dummyHead
        carry = 0
        while l1 or l2 or carry:
            l1_val = l1.val if l1 else 0
            l2_val = l2.val if l2 else 0
            # Calculate the sum of the current column along with carry
            columnSum = l1_val + l2_val + carry
            # Update carry for the next calculation
            carry = columnSum // 10
            # Create a new node with the value being the remainder of the sum
            cur.next = ListNode(columnSum % 10)
            # Move to the next nodes in the input lists (if available)
            l1 = l1.next if l1 else None
            l2 = l2.next if l2 else None
            # Move the current pointer to the next node
            cur = cur.next
        # Return the result starting from the next of the dummy head
        return dummyHead.next

            
 ```


### Analysis
start with dummyHead.next

use cur to refer to dummyHead

move to the next node when a new node is appended in (cur.next = ListNode(xxx), cur=cur.next)

return dummyHead.next

