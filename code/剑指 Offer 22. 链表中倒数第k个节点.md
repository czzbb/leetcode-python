# 剑指 Offer 22. 链表中倒数第k个节点
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/

**示例：**
```
给定一个链表: 1->2->3->4->5, 和 k = 2.

返回链表 4->5.
```

## 代码
```python
class j22_Solution:
    # 双指针
    # n2比n1快走k步，再一起走。n2走到null时，n1就是答案
    def getKthFromEnd(self, head: ListNode, k: int) -> ListNode:
        n1, n2 = head, head
        for _ in range(k):
            n2 = n2.next
        while n2:
            n1, n2 = n1.next, n2.next
        return n1
```
