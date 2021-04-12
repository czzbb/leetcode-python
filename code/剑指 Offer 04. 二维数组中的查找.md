# 剑指 Offer 04. 二维数组中的查找
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/

在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

**示例:**
```
现有矩阵 matrix 如下：
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
给定 target = 5，返回 true。
给定 target = 20，返回 false。
```

## 思路
* 同[240. 搜索二维矩阵 II](https://github.com/czzbb/leetcode-python/blob/master/code/0240-%E6%90%9C%E7%B4%A2%E4%BA%8C%E7%BB%B4%E7%9F%A9%E9%98%B5%20II.md)
* 从左下角或者右上角来看，就像一个二叉搜索树。
* 代码从左下角看，向上看都比自己小，向右看都比自己大。

## 代码
```python
class j4_Solution:
    def findNumberIn2DArray(self, matrix: List[List[int]], target: int) -> bool:
        if len(matrix) == 0 or len(matrix[0]) == 0:return False
        m, n = len(matrix), len(matrix[0])
        i, j = m-1, 0
        while i>=0 and j<n:
            if matrix[i][j] == target:
                return True
            elif matrix[i][j] > target:
                i-=1
            else:
                j+=1
        return False
```
