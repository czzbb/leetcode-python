# 剑指 Offer 49. 丑数
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/chou-shu-lcof/

我们把只包含质因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。

**示例:**
```
输入: n = 10
输出: 12
解释: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 是前 10 个丑数。
```

## 代码
```python
class j49_Solution:
    # 同264
    # 将p2, p3, p5 看成指针，指向的值分别乘上2、3、5后会大于现在算出的最大丑数，然后选择最小的那个添加到丑数中。
    # 然后更新p2, p3, p5:即保证对应的值乘上2、3、5后会大于现在算出的最大丑数
    def nthUglyNumber(self, n: int) -> int:
        dp = [0] * n
        dp[0] = 1 # 第一个丑数是1
        p2 = p3 = p5 = 0
        for i in range(1, n):
            dp[i] = min(dp[p2]*2, dp[p3]*3, dp[p5]*5)
            if dp[i] == dp[p2]*2:p2+=1
            if dp[i] == dp[p3]*3:p3+=1
            if dp[i] == dp[p5]*5:p5+=1
        return dp[-1]
```
