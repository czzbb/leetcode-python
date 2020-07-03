# 剑指 Offer 09. 用两个栈实现队列
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

**示例 1：**
```
输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]
```
**示例 2：**
```
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```
## 思路
* 就用两个栈，倒来倒去。。。

## 代码
```python
class m9_CQueue(object):

    def __init__(self):
        self.st1 = []
        self.st2 = []

    def appendTail(self, value):
        """
        :type value: int
        :rtype: None
        """
        self.st1.append(value)

    def deleteHead(self):
        """
        :rtype: int
        """
        if self.st2:
            return self.st2.pop()
        while self.st1:
            self.st2.append(self.st1.pop())
        if self.st2:
            return self.st2.pop()
        return -1
```
