<https://leetcode.com/problems/delete-node-in-a-linked-list/>

It is worth noting that the head node is not given in the input, so there is no way we could find the previous node of the given  `node` to be deleted. We can modify the value of the given `node` and all the following nodes with the value of the next nodes, and set the `next` pointer of the second last node to `None`.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def deleteNode(self, node):
        """
        :type node: ListNode
        :rtype: void Do not return anything, modify node in-place instead.
        """
        while node.next:
            node.val = node.next.val
            prev = node
            node = node.next
        prev.next = None
```

A better way is modifying the value of the `node` with its next, and set its `next` to the `next` of its `next`.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def deleteNode(self, node):
        """
        :type node: ListNode
        :rtype: void Do not return anything, modify node in-place instead.
        """
        node.val = node.next.val
        node.next = node.next.next
```

