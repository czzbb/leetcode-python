# 剑指 Offer 44. 数字序列中某一位的数字
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/

数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。

请写一个函数，求任意第n位对应的数字。

**示例 1：**
```
输入：n = 3
输出：3
```
**示例 2：**
```
输入：n = 11
输出：0
```

## 代码
```python
class j44_Solution:
    # 同400
    # 每种位数，共有 base*9*(10**(base-1)) 位
    # 例如2位数，有10-99共90*2=180位，即 2*9*10。
    # 这里下标从0开始算。解答中都是从1开始算的，所以有些不同。
    def findNthDigit(self, n: int) -> int:
        if n<10: return n # 小于10的直接返回
        # 否则从10，开始
        base = 2 # base 表示当前处理的位数
        left = n-10 # left表示还有多少位，从0开始
        while True:
            if left<base*9*(10**(base-1)): # 表示在当前位数
                ind1 = left//base # ind1 指向当前的数字
                ind2 = left%base  # ind2 指向数字中的第几位
                num = 10**(base-1) + ind1 # 当前的数字
                return int(str(num)[ind2])
            else: # 超过的当前位数，到下一位
                left -= base*9*(10**(base-1))
                base+=1
```
