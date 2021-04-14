# 剑指 Offer 10- I. 斐波那契数列
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/

写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项（即 F(N)）。斐波那契数列的定义如下：
```
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。
```
**示例 1：**
```
输入：n = 2
输出：1
```
**示例 2：**
```
输入：n = 5
输出：5
```

## 代码
```python
class j10_1_Solution:
    # 如果用递归方法，会有重复子问题，超时。
    def fib(self, n: int) -> int:
        if n < 2:return n
        dp1, dp2 = 0, 1
        for _ in range(n-1):
            dp1, dp2 = dp2, dp1+dp2
        return dp2%(10**9+7)
```
