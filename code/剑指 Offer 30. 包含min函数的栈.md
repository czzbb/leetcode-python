# 剑指 Offer 30. 包含min函数的栈
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

**示例:**
```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```

## 代码
```python
class j30_MinStack:
    def __init__(self):
        """
        initialize your data structure here.
        """
        self.st1 = [] # 数据栈
        self.st2 = [] # 辅助栈：单调栈

    def push(self, x: int) -> None:
        self.st1.append(x)
        #
        if len(self.st2) == 0 or x<= self.st2[-1]:
            self.st2.append(x)

    def pop(self) -> None:
        if self.st1:
            val = self.st1.pop()
            if val == self.st2[-1]:
                self.st2.pop()

    def top(self) -> int:
        if self.st1:
            return self.st1[-1]

    def min(self) -> int:
        if self.st2:
            return self.st2[-1]
```
