# 剑指 Offer 24. 反转链表
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

**示例:**
```
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

## 代码
```python
class j24_Solution(object):
    # 同206题
    # 这里先赋值cur.next，先赋值pre会出错。。不知道为什么
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        pre = None
        cur = head
        while cur:
            cur.next, pre, cur=pre, cur, cur.next
        return pre
```
```python
class j24__Solution:
    # 使用递归的方法
    def reverseList(self, head: ListNode) -> ListNode:
        if not head or not head.next: return head
        p = self.reverseList(head.next)
        head.next.next = head
        head.next = None
        return p
```
