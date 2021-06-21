# 剑指 Offer 65. 不用加减乘除做加法
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/

写一个函数，求两个整数之和，要求在函数体内不得使用 “+”、“-”、“*”、“/” 四则运算符号。

**示例:**
```
输入: a = 1, b = 1
输出: 2
```

## 代码
```python
class j65_Solution:
    # 二进制方法
    # 将 a 看成是本位，b 看成是进位
    # 本位是由异或得到；进位是由与得到，并且要右移1
    def add(self, a: int, b: int) -> int:
        mask = 0xffffffff
        a, b = a&mask, b&mask
        while b:
            a, b = (a^b), ((a&b)<<1)&mask
        return a if a<=0x7fffffff else ~(a^mask)
class j65__Solution:
    # 最后返回的表达更改了下，更好理解
    def add(self, a: int, b: int) -> int:
        mask = 0xffffffff
        a, b = a&mask, b&mask
        while b:
            a, b = (a^b), ((a&b)<<1)&mask
        return a if a<2**31 else a-2**32
```
