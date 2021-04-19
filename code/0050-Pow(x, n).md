# 50. Pow(x, n)
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/powx-n/

实现 pow(x, n) ，即计算 x 的 n 次幂函数。

**示例 1:**
```
输入: 2.00000, 10
输出: 1024.00000
```
**示例 2:**
```
输入: 2.10000, 3
输出: 9.26100
```
**示例 3:**
```
输入: 2.00000, -2
输出: 0.25000
解释: 2-2 = 1/22 = 1/4 = 0.25
```

## 思路
**方法一**
* 二分法
* `n` 小于`0`， 就 `x, n = 1 / x, -n`
* 例如：`x**37`(奇数)，则可以通过计算 `x**18 * x**18 * x`来得到；
* 而 `x**18`(偶数)，则可以通过计算 `x**9 * x**9` 来得到

**方法二**
* 利用位运算
* 即使用了`n`次`x`，可以将`n`的二进制写出来
* 例如`n`的二进制为：`1001101`，则最终使用了 `x**1 * x**4 * x**8 * x**64`

## 代码
**方法一**
```python
class a50_Solution:
    def myPow(self, x: float, n: int) -> float:
        if n < 0:
            n, x = -n, 1/x
        def func(n):
            if n == 0: return 1
            y = func(n>>1)
            if n&1:
                return x*y*y
            return y*y
        return func(n)
```
**方法二**
```python
class a50__Solution(object):
    def myPow(self, x: float, n: int) -> float:
        if n < 0:
            x, n = 1 / x, -n
        ans = 1
        base = x
        while n:
            if n & 1:
                ans *= base
            n >>= 1
            base *= base
        return ans
```
