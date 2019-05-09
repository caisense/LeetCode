# 链表总结

链表类题目：

[https://leetcode-cn.com/tag/linked-list/](https://leetcode-cn.com/tag/linked-list/)

## 用双指针法找中点：

### 1.有辅助头结点的：

```python
Head = ListNode(None)    #辅助头
Head.next = head    #真实头
slow = fast = Head
while fast.next and fast.next.next:
    fast = fast.next.next
    slow = slow.next
```

长度为偶：`H->1->2->3->4`

`slow`为中点（值为2）

长度为奇：`H->1->2->3->4->5`

`slow.next`为中点（值为3）

### 2.没有辅助头结点的：

```python
slow = fast = head
pre = None
while fast and fast.next:
    pre = slow
    fast = fast.next.next
    slow = slow.next
```

长度为偶：`1->2->3->4`

`slow`为3，其前驱`pre`为中点

长度为奇：`1->2->3->4->5`

`slow`为中点（值为3）

### 总结

有辅助头结点的，慢指针（或者其后继）指向中点，因此最终拿slow来用即可；

没有辅助头的，要设一个pre记录slow前驱，视链长奇偶来求中点。

