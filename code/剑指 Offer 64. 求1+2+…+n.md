# 剑指 Offer 64. 求1+2+…+n
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/qiu-12n-lcof/

求 1+2+...+n ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

**示例 1：**
```
输入: n = 3
输出: 6
```
**示例 2：**
```
输入: n = 9
输出: 45
```

## 代码
```python
class j64_Solution(object):
    # and 前面如果是0，就不会再执行后面的操作
    def __init__(self):
        self.ans = 0
    def sumNums(self, n):
        """
        :type n: int
        :rtype: int
        """
        n and self.sumNums(n-1)
        self.ans += n
        return self.ans

class j64__Solution:
    # 你听说过俄罗斯农民乘法吗(二进制的方法)
    # 计算n*(n+1)/2
    def sumNums(self, n: int) -> int:
        a, b = n, n+1
        ans = 0
        while b:
            if b&1:
                ans += a
            a <<= 1
            b >>= 1
        return ans>>1
```
