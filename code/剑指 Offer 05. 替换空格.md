# 剑指 Offer 05. 替换空格
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/

请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

**示例 1：**
```
输入：s = "We are happy."
输出："We%20are%20happy."
```

## 代码
```python
class j5_Solution:
    def replaceSpace(self, s: str) -> str:
        return s.replace(' ', '%20')
```
