# 剑指 Offer 47. 礼物的最大价值
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/

在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？

**示例 1:**
```
输入: 
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 12
解释: 路径 1→3→5→2→1 可以拿到最多价值的礼物
```

## 代码
```python
class j47_Solution:
    # dp
    # dp[i][j]表达到达grid[i][j]获利最大值
    # dp方程为：dp[i][j] = max(dp[i-1][j], dp[i][j-1])+grid[i][j]

    def maxValue(self, grid: List[List[int]]) -> int:
        m, n = len(grid), len(grid[0])
        ### 初始化dp
        dp = [[0]*n for _ in range(m)]
        dp[0][0] = grid[0][0]
        for i in range(1, m):
            dp[i][0] = dp[i-1][0] + grid[i][0]
        for j in range(1, n):
            dp[0][j] = dp[0][j-1] + grid[0][j]
        #
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])+grid[i][j]
        return dp[-1][-1]
```
```python
class j47__Solution:
    # 状态压缩
    # 多初始化一维，即dp[0]一直为0，作为边界
    def maxValue(self, grid: List[List[int]]) -> int:
        m, n = len(grid), len(grid[0])
        ### 初始化dp
        dp = [0]*(n+1)
        for i in range(m):
            for j in range(n):
                dp[j+1] = max(dp[j+1], dp[j]) + grid[i][j]
        return dp[-1]
```
