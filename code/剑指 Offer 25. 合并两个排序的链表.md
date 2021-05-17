# 剑指 Offer 25. 合并两个排序的链表
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/

输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

**示例1：**
```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

## 代码
```python
class j25_Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        top = ListNode(0)
        cur = top
        while l1 and l2:
            if l1.val < l2.val:
                cur.next = l1
                l1 = l1.next
            else:
                cur.next = l2
                l2 = l2.next
            cur = cur.next
        cur.next = l1 if l1 else l2
        return top.next
```
