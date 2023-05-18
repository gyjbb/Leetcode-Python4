# Leetcode-Python4
## 24. Swap Nodes in Pairs, 19. Remove Nth Node From End of List, 142
May 15, 2023  4h

The fourth day for Linked List. Today we will learn more about the linked list.\
The challenges today are about 

## 24. Swap Nodes in Pairs
[Reading link](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0024.%E4%B8%A4%E4%B8%A4%E4%BA%A4%E6%8D%A2%E9%93%BE%E8%A1%A8%E4%B8%AD%E7%9A%84%E8%8A%82%E7%82%B9.md)\
<img src="https://github.com/gyjbb/Leetcode-Python4/blob/main/Screen%20Shot%202023-05-17%20at%202.58.58%20PM.png" width="400" height="180">

> cur = dummy_head\
> step 1-2: since the current pointer will change, we need to save the linked list original order and the nodes. So the linked list will not break:\
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
For **deleting** the node in a linked list, the current pointer need to be at the node before the node that needs to be deleted. Then use the cur.next = cur.next.next to delete.\
Use **two pinters** here, a fast one and a slow one. The fast pointer will move (n+1) steps first. Then two pointers move together until the fast one points to null.

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






