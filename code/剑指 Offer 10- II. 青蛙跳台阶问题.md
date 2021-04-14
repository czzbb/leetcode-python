# 剑指 Offer 10- II. 青蛙跳台阶问题
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/

一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 n 级的台阶总共有多少种跳法。  
答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

**示例 1：**
```
输入：n = 2
输出：2
```
**示例 2：**
```
输入：n = 7
输出：21
```
**示例 3：**
```
输入：n = 0
输出：1
```

## 代码
```python
class j10_2_Solution:
    # 与上题相比，只是初始条件不同
    def numWays(self, n: int) -> int:
        if n<2:return 1
        dp1 = dp2 = 1
        for i in range(n-1):
            dp1, dp2 = dp2, dp2+dp1
        return dp2%1000000007
```
