# Leetcode-Python4
## 24. Swap Nodes in Pairs, 19. Remove Nth Node From End of List, Two connected linked lists, 142. Linked List Cycle II

May 15, 2023  4h

The fourth day for Linked List. Today we will learn more about the linked list.\
The challenges today are about 

## 24. Swap Nodes in Pairs
[Reading link](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0024.%E4%B8%A4%E4%B8%A4%E4%BA%A4%E6%8D%A2%E9%93%BE%E8%A1%A8%E4%B8%AD%E7%9A%84%E8%8A%82%E7%82%B9.md)\
<img src="https://github.com/gyjbb/Leetcode-Python4/blob/main/Screen%20Shot%202023-05-17%20at%202.58.58%20PM.png" width="400" height="180">

> cur = dummy_head\
> step 1-2: since the current pointer will change, we need to save original order and the nodes of the linked list using **temp pointer**. So the linked list will not break:\
> temp = cur.next\
> temp1 = cur.next.next.next\
> step 1 in the picture above:\
> cur.next = cur.next.next\
> step 2:\
> cur.next.next = temp\
> step 3:\
> temp.next = temp1\
> finally return the dummy head.next


```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy_head = ListNode(next=head)
        current = dummy_head

        # 必须有cur的下一个和下下个才能交换，否则说明已经交换结束了
        while current.next and current.next.next:
            temp = current.next # 防止节点修改
            temp1 = current.next.next.next

            current.next = current.next.next
            current.next.next = temp
            temp.next = temp1
            current = current.next.next
        return dummy_head.next
```


## 19. Remove Nth Node From End of List
[Leetcode Link](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)\
[Reading Link](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0019.%E5%88%A0%E9%99%A4%E9%93%BE%E8%A1%A8%E7%9A%84%E5%80%92%E6%95%B0%E7%AC%ACN%E4%B8%AA%E8%8A%82%E7%82%B9.md)\
For **deleting** the node in a linked list, the current pointer needs to be at the node before the node that needs to be deleted. Then use the cur.next = cur.next.next to delete.\
Use **two pointers** here, a fast one and a slow one. The fast pointer will move (n+1) steps first. Then two pointers move together until the fast one points to null.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy_head = ListNode(0, head)
        slow = fast = dummy_head
        # 快指针比慢指针快 n+1 步
        for i in range(n+1):
            fast = fast.next
        # 移动两个指针，直到快速指针到达链表的末尾
        while fast:
            slow = slow.next
            fast = fast.next
        
        # 通过更新第 (n-1) 个节点的 next 指针删除第 n 个节点
        slow.next = slow.next.next
        
        return dummy_head.next
```

## Interview question: two connected linked lists
[Reading link](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/%E9%9D%A2%E8%AF%95%E9%A2%9802.07.%E9%93%BE%E8%A1%A8%E7%9B%B8%E4%BA%A4.md)\
<img src="https://github.com/gyjbb/Leetcode-Python4/blob/main/Screen%20Shot%202023-05-17%20at%205.17.48%20PM.png" width="400" height="150">

```python
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        lenA = self.getLength(headA)
        lenB = self.getLength(headB)
        
        # 通过移动较长的链表，使两链表长度相等
        if lenA > lenB:
            headA = self.moveForward(headA, lenA - lenB)
        else:
            headB = self.moveForward(headB, lenB - lenA)
        
        # 将两个头向前移动，直到它们相交
        while headA and headB:
            if headA == headB:
                return headA
            headA = headA.next
            headB = headB.next
        
        return None
    
    def getLength(self, head: ListNode) -> int:
        length = 0
        while head:
            length += 1
            head = head.next
        return length
    
    def moveForward(self, head: ListNode, steps: int) -> ListNode:
        while steps > 0:
            head = head.next
            steps -= 1
        return head
```

## 142. Linked List Cycle II
[Leetcode link](https://leetcode.com/problems/linked-list-cycle-ii/)\
[Video link](https://www.bilibili.com/video/BV1if4y1d7ob/?spm_id_from=333.788&vd_source=63f26efad0d35bcbb0de794512ac21f3)
1. How to judge if a linked list has a loop?\
Here we can also use **two pointers**. A fast one and a slow one. The fast pointer moves 2 steps every time, and the slow one moves 1 step every time. If the linked list has a loop, the fast and slow pointers will meet in the loop.
2. How to find the start of the loop?\
[Reading link](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0142.%E7%8E%AF%E5%BD%A2%E9%93%BE%E8%A1%A8II.md)
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None
class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
        slow = head
        fast = head
        
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            
            # If there is a cycle, the slow and fast pointers will eventually meet.
            if slow == fast:
                # Move one of the pointers back to the start of the list
                slow = head
                while slow != fast:
                    slow = slow.next
                    fast = fast.next
                return slow
        # If there is no cycle, return None
        return None
```

## Linked List conclusion
1. [linked list theory](https://programmercarl.com/%E9%93%BE%E8%A1%A8%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)
2. dummy head
3. add and delete nodes in linked list
4. reverse a linked list
5. remove nth node from the end of linked list
6. two connected linked lists
7. linked list cycle.









