# 剑指 Offer 06. 从尾到头打印链表
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

**示例 1：**
```
输入：head = [1,3,2]
输出：[2,3,1]
```

## 代码
```python
class j6_Solution:
    # 递归法
    def reversePrint(self, head: ListNode) -> List[int]:
        if not head:return []
        return self.reversePrint(head.next)+[head.val]
```
```python
class j6__Solution:
    # 栈方法
    def reversePrint(self, head: ListNode) -> List[int]:
        ans = []
        while head:
            ans.append(head.val)
            head = head.next
        return ans[::-1]
```
