# 剑指 Offer 60. n个骰子的点数
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/nge-tou-zi-de-dian-shu-lcof/

把n个骰子扔在地上，所有骰子朝上一面的点数之和为s。输入n，打印出s的所有可能的值出现的概率。

你需要用一个浮点数数组返回答案，其中第 i 个元素代表这 n 个骰子所能掷出的点数集合中第 i 小的那个的概率。

**示例 1:**
```
输入: 1
输出: [0.16667,0.16667,0.16667,0.16667,0.16667,0.16667]
```
**示例 2:**
```
输入: 2
输出: [0.02778,0.05556,0.08333,0.11111,0.13889,0.16667,0.13889,0.11111,0.08333,0.05556,0.02778]
```

## 代码
```python
class j60_Solution:
    # dp[i][j] 表示用了i+1个骰子，得分为j+1的情况数
    # 状态转移方程：dp[i][j] = sum(dp[i-1][j-6:j])
    def dicesProbability(self, n: int) -> List[float]:
        dp = [[0]*6*n for _ in range(n)]
        for j in range(6):
            dp[0][j] = 1
        for i in range(1, n):
            for j in range(i, (i+1)*6):
                if j-6<0:
                    dp[i][j] = sum(dp[i-1][:j])
                else:
                    dp[i][j] = sum(dp[i-1][j-6:j])
        base = 6**n
        return [i/base for i in dp[-1][n-1:]]
class j60__Solution:
    # 压缩状态空间
    def dicesProbability(self, n: int) -> List[float]:
        dp = [0] * 6 * n
        for j in range(6):
            dp[j] = 1
        for i in range(1, n):
            for j in range((i+1)*6-1, i-1, -1):
                # 这里需要倒叙遍历
                if j-6<0:
                    dp[j] = sum(dp[:j])
                else:
                    dp[j] = sum(dp[j-6:j])
            dp[i-1] = 0 # 需要将不可能的结果置零
        base = 6**n
        return [i/base for i in dp[n-1:]]
```
