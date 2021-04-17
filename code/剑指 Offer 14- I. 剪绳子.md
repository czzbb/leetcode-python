# 剑指 Offer 14- I. 剪绳子
**难度: Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/jian-sheng-zi-lcof/

给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m-1] 。请问 k[0]*k[1]*...*k[m-1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

**示例 1：**
```
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1
```
**示例 2:**
```
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36
```

## 代码
```python
class j14_1_Solution:
    # 数论
    # 将绳子分为 相等 的多段，乘机最大。根据算术几何均值不等式的取等条件
    # 将绳子尽可能分为长为3的多段，乘积最大
    # 若有余1，因为3*1<2*2，则将最后一个长度3，1变为2，2
    # 若有余2，则直接乘2
    def cuttingRope(self, n: int) -> int:
        if n<=3: return n-1
        a, b = n//3, n%3
        if b == 0: return int(math.pow(3, a)) # 刚好
        if b == 1: return int(math.pow(3, a-1)*4) # 余1
        return int(math.pow(3,a)*2) # 余2
```
```python
class j14_1__Solution:
    # 递归穷举
    # f(n) = max(i*f(n-i), i*(n-i))
    # 即将n拆分为i + (n-i), i=2,...,n-2。因为不会拆为1，所以从2开始。
    # max中第一部分表示n-i要继续拆分,第二部分表示不拆分了
    # 该方法会出现大量重复子问题
    def cuttingRope(self, n: int) -> int:
        if n<=3: return n-1
        def func(n):
            if n==2: return 1
            ans = 0
            for i in range(2, n-1):
                ans = max(ans, i*func(n-i), i*(n-i))
            return ans
        return func(n)
```
```python
class j14_1___Solution:
    # 带记忆的递归
    def cuttingRope(self, n: int) -> int:
        if n <= 3: return n - 1
        def func(n):
            if dp[n] == 0:
                ans = 0
                for i in range(2, n-1):
                    ans = max(ans, i*func(n-i), i*(n-i))
                dp[n] = ans
            return dp[n]
        dp = [0] * (n+1)
        dp[2] = 1
        return func(n)
```
```python
class j14_1____Solution:
    # 改为dp算法
    def cuttingRope(self, n: int) -> int:
        if n <= 3: return n - 1
        dp = [0]*(n+1)
        dp[2] = 1
        for i in range(3, n+1):
            for j in range(2, i-1):
                dp[i] = max(dp[i], j*dp[i-j], j*(i-j))
        return dp[n]
```
