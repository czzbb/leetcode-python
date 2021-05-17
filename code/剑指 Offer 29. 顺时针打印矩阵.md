# 剑指 Offer 29. 顺时针打印矩阵
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

**示例 1：**
```
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]
```
**示例 2：**
```
输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]
```

## 代码
```python
class j29_Solution:
    # 同54题
    # 设立上下左右四个边界，根据边界依次遍历
    def spiralOrder(self, matrix:[[int]]) -> [int]:
        if not matrix: return []
        l, r, t, b, res = 0, len(matrix[0]) - 1, 0, len(matrix) - 1, []
        while True:
            for i in range(l, r + 1): res.append(matrix[t][i]) # left to right
            t += 1
            if t > b: break
            for i in range(t, b + 1): res.append(matrix[i][r]) # top to bottom
            r -= 1
            if l > r: break
            for i in range(r, l - 1, -1): res.append(matrix[b][i]) # right to left
            b -= 1
            if t > b: break
            for i in range(b, t - 1, -1): res.append(matrix[i][l]) # bottom to top
            l += 1
            if l > r: break
        return res
```
```python
class j29__Solution:
    # 每次输出第一行，然后删去第一行，将矩阵逆时针旋转
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        ans = []
        while matrix:
            ans += matrix.pop(0)
            matrix = list(zip(*matrix))[::-1] # 矩阵旋转
        return ans
```
