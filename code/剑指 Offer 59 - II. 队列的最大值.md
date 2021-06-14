# 剑指 Offer 59 - II. 队列的最大值
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/

请定义一个队列并实现函数 max_value 得到队列里的最大值，要求函数max_value、push_back 和 pop_front 的均摊时间复杂度都是O(1)。

若队列为空，pop_front 和 max_value 需要返回 -1

**示例 1：**
```
输入: 
["MaxQueue","push_back","push_back","max_value","pop_front","max_value"]
[[],[1],[2],[],[],[]]
输出: [null,null,null,2,1,2]
```
**示例 2：**
```
输入: 
["MaxQueue","pop_front","max_value"]
[[],[],[]]
输出: [null,-1,-1]
```


## 代码
```python
class j59_2_MaxQueue:
    # 同上，利用单调（递减）栈
    def __init__(self):
        self.q = collections.deque()
        self.max_q = collections.deque() # 单调递减栈

    def max_value(self) -> int:
        if not self.max_q:return -1
        return self.max_q[0]

    def push_back(self, value: int) -> None:
        self.q.append(value)
        while self.max_q and self.max_q[-1]<value:
            self.max_q.pop()
        self.max_q.append(value)

    def pop_front(self) -> int:
        if not self.q:return -1
        value = self.q.popleft()
        if value == self.max_q[0]:
            self.max_q.popleft()
        return value
```
