# 剑指 Offer 18. 删除链表的节点
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/shan-chu-lian-biao-de-jie-dian-lcof/

给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。  
返回删除后的链表的头节点。  
注意：此题对比原题有改动

**示例 1:**
```
输入: head = [4,5,1,9], val = 5
输出: [4,1,9]
解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
```
## 代码
```python
class j18_Solution:
    # 遍历节点，直到值为val
    # 若val是节点，考虑如何在O(1)时间内删除
    def deleteNode(self, head: ListNode, val: int) -> ListNode:
        top = ListNode(0) # 创建头节点，以防删除的节点是首节点
        top.next = head
        pre, cur = top, head
        while cur and cur.val != val:
            pre, cur = cur, cur.next
        pre.next = cur.next
        return top.next
```
